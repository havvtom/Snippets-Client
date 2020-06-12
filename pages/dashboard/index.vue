<template>
	<div class="container mt-16">
		<div class="flex justify-between">
			<h1 class="text-xl font-medium text-gray-600 mb-6">
				Your snippets (1)
			</h1>
			<a href="#" @click.prevent="createSnippet">+ Create a Snippet</a>
		</div>		
	</div>
</template>
<script type="text/javascript">
export default {
	methods: {
		async createSnippet () {
			let snippet = await this.$axios.$post('snippets')

			this.$router.push({
				name: 'snippets-id-edit',
				params: {
					id: snippet.data.uuid
				}
			})
		}
	}
}
</script>