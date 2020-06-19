<template>
	<a
		href="#"
		@click="addStep"
		:to="{}"
		class="block mb-2 p-3 bg-blue-500 rounded-lg"
		:title="`Add Step ${position}`"
	>
		<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
			<path fill-rule="evenodd" d="M10 3a1 1 0 011 1v5h5a1 1 0 110 2h-5v5a1 1 0 11-2 0v-5H4a1 1 0 110-2h5V4a1 1 0 011-1z" clip-rule="evenodd"/>
		</svg>
	</a>
</template>
<script type="text/javascript">
	export default {
		props: {
			position: {
				required: true,
				type: String
			},
			snippet: {
				required: true,
				type: Object
			},
			currentStep: {
				required:true,
				type: Object
			}
		},
		methods: {
			async addStep () {
				let response = await this.$axios.$post(`/snippets/${this.snippet.uuid}/steps`, {
					[this.position]: this.currentStep.uuid
				})

				this.$emit('added', response.data)
			}
		}
	}
</script>