<template>
	<div>
		<div class="bg-white mb-16">
			<div class="container py-10 pb-16">
				<div class="w-10/12">
					<h1 class="text-4xl text-gray-700 font-medium leading-tight mb-4">Snippet Title</h1>
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
			<h1 class="text-xl text-gray-600 font-medium mb-6">
				1/1. Step Title
			</h1>
			<div class="flex flex-wrap lg:flex-no-wrap">
				<div class="flex flex-wrap lg:flex-no-wrap justify-between items-start w-full lg:w-8/12 lg:mr-16 mb-8">
					<div class="order-first">
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 rounded-lg mr-2"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M9.707 16.707a1 1 0 01-1.414 0l-6-6a1 1 0 010-1.414l6-6a1 1 0 011.414 1.414L5.414 9H17a1 1 0 110 2H5.414l4.293 4.293a1 1 0 010 1.414z" clip-rule="evenodd"/>
							</svg>
						</nuxt-link>
					</div>
					<div class="bg-white p-8 rounded-lg text-gray-600 w-full">
						Markdown Content
					</div>
					<div class="flex lg:flex-col flex-row order-first lg:order-last">
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 rounded-lg ml-2"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
								<path fill-rule="evenodd" d="M12.293 5.293a1 1 0 011.414 0l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-2.293-2.293a1 1 0 010-1.414z" clip-rule="evenodd"/>
							</svg>
						</nuxt-link>
						<nuxt-link
							:to="{}"
							class="block mb-2 p-3 bg-blue-500 order-first lg:order-last rounded-lg ml-2"
							title="Edit Step"
						>
							<svg viewBox="0 0 20 20" class="text-white h-6 w-6" fill="currentColor">
							  <path d="M17.414 2.586a2 2 0 00-2.828 0L7 10.172V13h2.828l7.586-7.586a2 2 0 000-2.828z"/>
							  <path fill-rule="evenodd" d="M2 6a2 2 0 012-2h4a1 1 0 010 2H4v10h10v-4a1 1 0 112 0v4a2 2 0 01-2 2H4a2 2 0 01-2-2V6z" clip-rule="evenodd"/>
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
								v-for="(step, index) in 5" 
								:key="index"
							>
								<nuxt-link
									:to="{}"
									:class="{
										'font-bold': index === 0
									}"
								>
									{{ index+1 }}. Step Title
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
export default {

}
</script>