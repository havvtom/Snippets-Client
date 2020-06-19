<template>
	<nuxt-link
		:to="step ? {
			query: {
				step: step.uuid
			}
		} : {}"
		class="block mb-2 p-3 bg-blue-500 rounded-lg"
		:class="{
			'opacity-25 pointer-events-none': !step
		}"
	>
		<slot/>
	</nuxt-link>
</template>
<script type="text/javascript">
	export default {
		props: {
			step: {
				type: Object
			}
		}
	}
</script>