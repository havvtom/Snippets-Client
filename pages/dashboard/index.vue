<template>
	<div class="container mt-16">
		<div class="flex justify-between">
			<h1 class="text-xl font-medium text-gray-600 mb-6">
				Your snippets ({{snippets.length}})
			</h1>
			<a href="#" @click.prevent="createSnippet">+ Create a Snippet</a>
		</div>	
		<div v-if="snippets.length === 0" class="text-gray-500 font-medium">
			There are no snippets here. Why don't you make one?
		</div>
		<dashboard-snippet-card
			v-for="(snippet, index) in snippets"
			:key="index"
			:snippet="snippet"
			@deleted="removeSnippet"
		/>	
	</div>
</template>
<script type="text/javascript">
import DashboardSnippetCard from './components/DashboardSnippetCard'
export default {
	data () {
		return {
			snippets: []
		}
	},
	middleware: ['auth'],
	head () {
	  return {
	    title: 'Dashboard',
	  }
	},
	components: {
		DashboardSnippetCard
	},
	methods: {
		async createSnippet () {
			let snippet = await this.$axios.$post('snippets')

			this.$router.push({
				name: 'snippets-id-edit',
				params: {
					id: snippet.data.uuid
				}
			})
		},
		removeSnippet (snippet) {
			this.snippets = this.snippets.filter( (s) => s.uuid !== snippet.uuid)
		}
	},
	async asyncData ({ app }) {
			let snippets = await app.$axios.$get('me/snippets')

			return {
				snippets: snippets.data
			}
		}

	}
</script>