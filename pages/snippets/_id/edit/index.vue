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
				<div class="text-xl text-gray-600 font-medium mr-3">
					1/1. 
				</div>
				<input 
					type="text"  
					value="" 
					class="text-xl text-gray-600 border-gray-400 font-medium py-1 bg-transparent px-2 border-2 rounded w-full"
					placeholder="Untitled Step" 
					v-model="currentStep.title"
				>
			</div>
			
			<div class="flex flex-wrap lg:flex-no-wrap">
				<div class="flex flex-wrap lg:flex-no-wrap justify-between items-start w-full lg:w-8/12 lg:mr-16 mb-8">
					<div class="flex flex-row lg:flex-col order-first">
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 rounded-lg mr-2"
							title="Previous Step"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z" clip-rule="evenodd"/>
							</svg>
						</nuxt-link>
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 rounded-lg mr-2"
							title="Add Step Before"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd"/>
							</svg>
						</nuxt-link>
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
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 rounded-lg ml-2 order-last lg:order-first"
							title="Next Step"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
							</svg>
						</nuxt-link>
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 rounded-lg ml-2"
							title="Add Step After"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd"/>
							</svg>
						</nuxt-link>
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 order-first lg:order-last rounded-lg ml-2"
							title="Delete Step"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
							  <path fill-rule="evenodd" d="M9 2a1 1 0 00-.894.553L7.382 4H4a1 1 0 000 2v10a2 2 0 002 2h8a2 2 0 002-2V6a1 1 0 100-2h-3.382l-.724-1.447A1 1 0 0011 2H9zM7 8a1 1 0 012 0v6a1 1 0 11-2 0V8zm5-1a1 1 0 00-1 1v6a1 1 0 102 0V8a1 1 0 00-1-1z" clip-rule="evenodd"/>
							</svg>
						</nuxt-link>
					</div>
				</div>
				<div class="w-full lg:w-4/12">
					<div class="mb-8">
						<h1 class="text-xl text-gray-600 font-medium mb-6">
							Steps
						</h1>
						<ul>
							<li 
								class="mb-1" 
								v-for="(step, index) in orderedStepsAsc" 
								:key="index"
							>
								<nuxt-link
									:to="{}"
									:class="{
										'font-bold': currentStep.uuid === step.uuid
									}"
								>
									{{ index+1 }}. {{step.title || 'Untitled step'}}
								</nuxt-link>
							</li>
						</ul>
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
import { orderBy as _orderBy } from 'lodash'
import { debounce as _debounce } from 'lodash'
export default {
	data () {
		return {
			snippet: null,
			steps: []
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
			}, 500)
		},
		currentStep: {
			deep: true,

			handler: _debounce( async function (step) {
				await this.$axios.$patch(`/snippets/${this.snippet.uuid}/steps/${step.uuid}`, {
					title: step.title, 
					body: step.body
				})
			}, 500)
		}
	},
	computed: {
		orderedStepsAsc () {
			return _orderBy (
				this.steps, 'order', 'asc'
				)
		},
		firstStep () {
			return this.orderedStepsAsc[0]
		},
		currentStep () {
			return this.orderedStepsAsc.find(
				(s) => s.uuid === this.$route.query.step
				) || this.firstStep
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