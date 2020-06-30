<template>
		<snippet-card
		:snippet="snippet"	
		>
			<nuxt-link 
				:to="{}"
			>
				{{ snippet.author.data.name }}
			</nuxt-link>
		</snippet-card>
</template>
<script type="text/javascript">
	import SnippetCard from '@/components/snippets/SnippetCard'
	export default {
		props: {
			snippet: {
				required: true,
				type: Object
			}
		},
		components: {
			SnippetCard
		}
	}
</script>