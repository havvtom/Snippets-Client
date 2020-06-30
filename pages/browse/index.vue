<template>
	<div class="">
		<div class="mb-16 bg-white">
			<div class="container py-10 pb-16">
				<h1 class="text-4xl text-gray-700 font-medium leading-tight mb-4">
					Browse
				</h1>				
			</div>			
		</div>
		<div class="container">
			<h1 class="text-xl font-medium text-gray-600 mb-6">
				All snippets ({{snippets.length}})
			</h1>
			<browse-snippet-card
				v-for="(snippet, index) in snippets"
				:key="index"
				:snippet="snippet"
			/>
		</div>
	</div>
</template>

<script type="text/javascript">
	import BrowseSnippetCard from './components/BrowseSnippetCard'
	export default {
		data () {
			return {
				snippets: []
			}
		},
		head () {
		  return {
		    title: 'Browse',
		  }
		},
		components: {
			BrowseSnippetCard
		},
		async asyncData ({ app }) {
			let snippets = await app.$axios.$get('snippets')

			return {
				snippets: snippets.data
			}
		}
	}
</script>