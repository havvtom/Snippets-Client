<template>
  <div class="">
    <div class="bg-white mb-16">
    	<div class="container flex py-16 lg:py-32">
    		<div class="w-full lg:w-6/12">
    			<h1 class="text-5xl font-medium text-gray-700 leading-tight mb-6">
    				Browse and create step by step mini tutorials
    			</h1>
    			<p class="text-xl text-gray-600 mb-12">
    				He who partakes of this shall not fail
    			</p>
    			<nuxt-link
    				:to="{
    					name: 'snippets-id',
    					params: {
    						id: SNIPPET_EXAMPLE_UUID
    					}
    				}"
    				class="inline-block text-lg py-3 px-5 bg-blue-500 text-white rounded-lg"
    			>
    				Check out an example &rarr;
    			</nuxt-link>
    		</div>
    	</div>    	
    </div>
    <div class="container">
		<h1 class="text-xl font-medium text-gray-600 mb-6">
			Latest Snippets
		</h1>
		<latest-snippet-card
			v-for="(snippet, index) in snippets"
			:key="index"
			:snippet="snippet"
		/>
	</div>
  </div>
</template>

<script>

import LatestSnippetCard from './home/components/LatestSnippetCard'
export default {
	components: {
		LatestSnippetCard
	},
	data () {
		return {
			snippets: [],
			SNIPPET_EXAMPLE_UUID: process.env.SNIPPET_EXAMPLE_UUID
		}
	},
	 head () {
	  return {
	    title: 'Snippets by HavvTom',
	    titleTemplate: ''
	  }
	 },
	 async asyncData ({ app }) {
	 	let snippets = await app.$axios.$get('snippets?limit=10')

	 	return {
	 		snippets: snippets.data
	 	}
	 }
}
</script>


