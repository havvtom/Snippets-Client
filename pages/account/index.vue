<template>
	<div class="container mt-16">
		<div class="flex flex-col items-center">
			<h1 class="text-3xl text-gray-700 font-medium mb-10">{{ $auth.user.name }}</h1>
			<div class="w-full md:w-6/12 lg:w-5/12 mb-6">			
				<form 
					action="#" 
					class="mb-6"
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
					<div class="mb-6">
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
						<div class="text-sm text-gray-500">
							Leave blank to keep the same
						</div>
					</div>
					<div>
						<button
							class="bg-blue-500 uppercase text-white text-center p-4 rounded"
						>
							Update
						</button>
					</div>							
				</form>
				<div class="">
					<nuxt-link
						:to="{
							name: 'author-id',
							params: {
								id: $auth.user.username
							}
						}"
					>
						View your Profile here
					</nuxt-link>
				</div>
			</div>
		</div>
	</div>
</template>
<script type="text/javascript">
export default {
	data () {
		return {
			form: {
				email: this.$auth.user.email,
				name: this.$auth.user.name,
				username: this.$auth.user.username,
				password: ''
			},
			validation: {

			}
		}
	},
	head () {
		return {
			title: 'Account'
		}
	},
	methods: {
		async submit () {
			try {
				await this.$axios.$patch(`users/${this.$auth.user.username}`, this.form) 
				await this.$auth.fetchUser()

				this.form.password = ''
				this.validation = {}
			} catch (e) {
				if(e.response.status === 422) {
					this.validation = e.response.data.errors
				}
			}
			
		}
	},
	mounted () {
		
	}
} 
</script>