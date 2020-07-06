<template>
	<div class="">
		<div class="mb-16 bg-white">
			<div class="container py-10 pb-16">
				<h1 class="text-4xl text-gray-700 font-medium leading-tight mb-4">
					{{user.name}}
				</h1>	
				<div class="text-gray-600">
					Member since {{ joinedAt }}
				</div>			
			</div>			
		</div>
		<div class="container">
			<h1 class="text-xl font-medium text-gray-600 mb-6">
				Public snippets ({{ snippets.length }})
			</h1>
			<snippet-card
				v-for="(snippet, index) in snippets"
				:key="index"
				:snippet="snippet"
			/>
		</div>
	</div>
</template>

<script type="text/javascript">
	import moment from 'moment'
	import SnippetCard from "@/components/snippets/SnippetCard"
	export default {
		data () {
			return {
				user: null,
				snippets: []
			}
		},
		head () {
			return {
				title: `Snippets by ${this.user.name}`
			}
		},
		computed: {
			joinedAt () {
				return moment(this.user.joined_at, 'YYYY-MM-DD hh::mm::ss').format('Do MMMM YYYY')
			}
		},
		components: {
			SnippetCard
		},
		async asyncData ({ app, params }) {
			let user = await app.$axios.$get(`users/${params.id}`)
			let snippets = await app.$axios.$get(`users/${params.id}/snippets`)

			return {
				user: user.data,
				snippets: snippets.data
			}
		}
	}
</script>