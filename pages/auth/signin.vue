<template>
	<div class="container mt-16">
		<div class="flex flex-col items-center">
			<h1 class="text-3xl text-gray-700 font-medium mb-10">Hello.</h1>
			<form 
				action="#" 
				class="bg-white rounded p-8 w-full md:w-6/12 lg:w-5/12 mb-6"
				@submit.prevent="submit"
			>
				<div class="mb-6">
					<label 
						for="email"
						class="block text-gray-600 font-medium mb-2" 
						:class="{
							'text-red-500': validation.email
						}"
					>
						Email Address
					</label>
					<input 
						type="text" 
						name="email" 
						id="email"
						class="border-2 border-gray-400 block w-full p-3" 
						:class="{
							'border-red-500': validation.email
						}"
						v-model="form.email"
					>
					<div v-if="validation.email" class="text-red-500 mb-4 text-sm mt-1">
						{{validation.email[0]}}
					</div>
				</div>
				<div class="mb-6">
					<label 
						for="password"
						class="block text-gray-600 font-medium mb-2" 
						:class="{
							'text-red-500': validation.password
						}"
					>
						Password
					</label>
					<input 
						type="password" 
						name="password" 
						id="password"
						class="border-2 border-gray-400 block w-full p-3" 
						:class="{
							'border-red-500': validation.password
						}"
						v-model="form.password"
					>
					<div class="text-red-500 mb-4 text-sm mt-1" v-if="validation.password">
						{{validation.password[0]}}
					</div>
				</div>
				<div>
					<button
						class="bg-blue-500 w-full uppercase text-white text-center p-4 rounded"
					>
						Sign In
					</button>
				</div>							
			</form>
			<div class="text-center text-gray-600">
				No Account?
				<nuxt-link
					:to="{ name: 'index' }"
				>
					Create one here
				</nuxt-link>
			</div>
		</div>
	</div>
</template>
<script type="text/javascript">
export default {
	data () {
		return {
			form: {
				email: '',
				password: ''
			},
			validation: {

			}
		}
	},
	head () {
		return {
			title: 'SignIn'
		}
	},
	methods: {
		async submit () {
			try {
				await this.$auth.loginWith('local', {
				data: this.form
				})
			} catch (e) {
				if(e.response.status === 422) {
					this.validation = e.response.data.errors
				}
			}
			
		}
	}
}
</script>