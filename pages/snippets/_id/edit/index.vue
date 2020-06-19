<template>
	<div>
		<div class="bg-white mb-16">
			<div class="container py-10 pb-16">
				<div class="w-10/12">
					<input 
						type="text"
						class="font-header w-full block p-2 border-2 rounded text-4xl text-gray-700 font-medium leading-tight mb-4 border-gray-400" 
						value=""
						placeholder="Untitled Snippet" 
						v-model="snippet.title"
					/>
					<div class="text-gray-600">
						Created by
						<nuxt-link
							:to="{}"
						>
							Tom Havv
						</nuxt-link>
					</div>
				</div>
			</div>
		</div>
		<div class="container">
			<div class="flex items-center mb-6">
				<div class="text-xl text-gray-600 font-header font-medium mr-3">
					{{ currentStepIndex + 1 }}/{{ steps.length }}. 
				</div>
				<input 
					type="text"  
					value="" 
					class="text-xl text-gray-600 border-gray-400 font-header font-medium py-1 bg-transparent px-2 border-2 rounded w-full"
					placeholder="Untitled Step" 
					v-model="currentStep.title"
				>
			</div>
			
			<div class="flex flex-wrap lg:flex-no-wrap">
				<div class="flex flex-wrap lg:flex-no-wrap justify-between items-start w-full lg:w-8/12 lg:mr-16 mb-8">
					<div class="flex flex-row lg:flex-col order-first">
						<step-navigation-button
							:step="previousStep"
							class="mr-2"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z" clip-rule="evenodd"/>
							</svg>
						</step-navigation-button>
						<add-step-button
							class="mr-2"
							position="before"
							:snippet="snippet"
							:currentStep="currentStep"
							@added="handleStepAdded"
						/>
					</div>
					<div class="w-full">
						<textarea 
							class="w-full mb-6 border-2 border-gray-400 rounded"
							v-model="currentStep.body"
						>
						</textarea>
						<div class="bg-white p-8 rounded-lg text-gray-600 ">
							Markdown Content
						</div>
					</div>
					
					<div class="flex lg:flex-col flex-row order-first lg:order-last">
						<step-navigation-button
							:step="nextStep"
							class="ml-2"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
							</svg>
						</step-navigation-button>
						<add-step-button
							class="ml-2"
							position="after"
							:snippet="snippet"
							:currentStep="currentStep"
							@added="handleStepAdded"
						/>
						<delete-step-button
							:snippet="snippet"
							:step="currentStep"
							v-if="steps.length > 1"
							@deleted="handleStepDeleted"
						/>
					</div>
				</div>
				<div class="w-full lg:w-4/12">
					<div class="mb-8">
						<h1 class="text-xl text-gray-600 font-medium mb-6">
							Steps
						</h1>
						<step-list
							:steps="orderedStepsAsc"
							:currentStep="currentStep"
						/>
					</div>
					<div class="border-t-2 border-gray-300 py-6">
						<h1 class="text-xl text-gray-600 font-medium mb-6">
							Publishing
						</h1>
						<div class="text-gray-500 text-sm mb-6">
							<template v-if="lastSaved">
								Last saved at {{lastSavedFormatted}}
							</template>
							<template v-else>
								No changes saved in this session yet
							</template>
						</div>
						<div class="flex items-baseline">
							<input 
								type="checkbox" 
								name="public" 
								id="public" 
								class="mr-2"
								v-model="snippet.is_public"
							>
							<div>
								<label for="public" class="text-gray-600 font-medium">
									Make this snippet public
								</label>
								<div class="text-gray-500 text-sm">
									Don't worry you can change this later
								</div>
							</div>
						</div>
					</div>
					<div class="text-gray-500 text-sm">
						Use <div class="text-gray-600 leading-relaxed inline-block bg-gray-400 rounded-lg text-sm px-2">ctrl</div> + <div class="text-gray-600 leading-relaxed inline-block bg-gray-400 rounded-lg text-sm px-2">shift</div> + <div class="text-gray-600 leading-relaxed inline-block bg-gray-400 rounded-lg text-sm px-2">left or right</div> to navigate between steps
					</div>
				</div>
			</div>
		</div>
	</div>
</template>
<script type="text/javascript">

import { debounce as _debounce } from 'lodash'
import StepList from '../components/StepList'
import StepNavigationButton from '../components/StepNavigationButton'
import AddStepButton from './components/AddStepButton'
import DeleteStepButton from './components/DeleteStepButton'
import browseSnippet from '@/mixins/snippets/browseSnippet'
import moment from 'moment'

export default {
	components:{
		StepList,
		AddStepButton,
		StepNavigationButton,
		DeleteStepButton
	},
	data () {
		return {
			snippet: null,
			steps: [],
			lastSaved: null
		}
	},
	head () {
		return {
			title: `Editing ${this.snippet.title || 'Untitled Snippet'}`
		}
	},
	watch: {
		'snippet.title': {
			handler: _debounce( async function (title) {
				await this.$axios.$patch(`/snippets/${this.snippet.uuid}`, {title})

				this.touchLastSaved()
			}, 500)
		},
		'snippet.is_public': {
			handler: _debounce( async function (isPublic) {
				await this.$axios.$patch(`/snippets/${this.snippet.uuid}`, {
					is_public: isPublic})

				this.touchLastSaved()
			}, 500)
		},
		currentStep: {
			deep: true,

			handler: _debounce( async function (step) {
				await this.$axios.$patch(`/snippets/${this.snippet.uuid}/steps/${step.uuid}`, {
					title: step.title, 
					body: step.body
				})

				this.touchLastSaved()
			}, 500)
		}
	},
	mixins: [
		browseSnippet
	],
	computed: {
		lastSavedFormatted () {
			return moment(this.lastSaved).format("YYYY-MM-DD HH:mm:ss")
		}
	},
	methods: {
		touchLastSaved () {
			this.lastSaved = moment.now()
		},
		handleStepAdded (step) {
			this.steps.push(step)
			this.goToStep(step)
		},
		handleStepDeleted (step) {

			let previousStep = this.previousStep

			this.steps = this.steps.filter( (s) => {
				return s.uuid != step.uuid
			})

			this.goToStep(previousStep || this.firstStep)
		}
	},
	async asyncData ({ app, params }) {
		let snippet = await app.$axios.$get(`snippets/${params.id}`)

		return {
			snippet: snippet.data,
			steps: snippet.data.steps.data
		}
	}

}
</script>