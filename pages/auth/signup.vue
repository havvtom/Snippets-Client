<template>
	<div class="container mt-16">
		<div class="flex flex-col items-center">
			<h1 class="text-3xl text-gray-700 font-medium mb-10">Get Snippeting.</h1>
			
			<form 
				action="#" 
				class="bg-white rounded p-8 w-full md:w-8/12 lg:w-7/12 mb-6"
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
				<div class="flex flex-wrap lg:flex-no-wrap">
					<div class="lg:mr-6 w-full lg:w-6/12 mb-6">
						<label 
						for="name"
						class="block text-gray-600 font-medium mb-2" 
						:class="{
							'text-red-500': validation.name
						}"
					>
						Name
					</label>
					<input 
						type="text" 
						name="name" 
						id="name"
						class="border-2 border-gray-400 block w-full p-3" 
						:class="{
							'border-red-500': validation.name
						}"
						v-model="form.name"
					>
					<div v-if="validation.name" class="text-red-500 mb-4 text-sm mt-1">
						{{validation.name[0]}}
					</div>
					</div>
					<div class="w-full lg:w-6/12 mb-6">
						<label 
						for="username"
						class="block text-gray-600 font-medium mb-2" 
						:class="{
							'text-red-500': validation.username
						}"
					>
						Username
					</label>
					<input 
						type="text" 
						name="username" 
						id="username"
						class="border-2 border-gray-400 block w-full p-3" 
						:class="{
							'border-red-500': validation.username
						}"
						v-model="form.username"
					>
					<div v-if="validation.username" class="text-red-500 mb-4 text-sm mt-1">
						{{validation.username[0]}}
					</div>
					</div>
				</div>
				<div class="flex flex-wrap lg:flex-no-wrap">
					<div class="lg:mr-6 w-full lg:w-6/12 mb-6">
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
					<div v-if="validation.password" class="text-red-500 mb-4 text-sm mt-1">
						{{validation.password[0]}}
					</div>
					</div>
					<div class="w-full lg:w-6/12 mb-6">
						<label 
						for="password_confirmation"
						class="block text-gray-600 font-medium mb-2" 
						:class="{
							'text-red-500': validation.password_confirmation
						}"
					>
						Confirm Password
					</label>
					<input 
						type="password" 
						name="password_confirmation" 
						id="password_confirmation"
						class="border-2 border-gray-400 block w-full p-3" 
						:class="{
							'border-red-500': validation.password_confirmation
						}"
						v-model="form.password_confirmation"
					>
					<div v-if="validation.password_confirmation" class="text-red-500 mb-4 text-sm mt-1">
						{{validation.password_confirmation[0]}}
					</div>
					</div>
				</div>
				<div>
					<button
						class="bg-blue-500 w-full uppercase text-white text-center p-4 rounded"
					>
						Sign Up
					</button>
				</div>							
			</form>
			<div class="text-center text-gray-600">
				Already have an account?
				<nuxt-link
					:to="{ name: 'auth-signin' }"
				>
					Sign in here
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
				name: '',
				username: '',
				password: '',
				password_confirmation: ''
			},
			validation: {

			}
		}
	},
	head () {
		return {
			title: 'Sign Up'
		}
	},
	methods: {
		async submit () {
			try {
				await this.$axios.$post('auth/signup', this.form)

				await this.$auth.loginWith('local', {
				data: {
					email: this.form.email,
					password: this.form.password
				}
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