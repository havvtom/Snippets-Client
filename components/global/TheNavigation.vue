<template>
	<div class="bg-white py-8 lg:py-0 flex items-center">
		<div class="container flex flex-wrap lg:flex-no-wrap items-center">
			<nuxt-link
				:to="{ name: 'index' }"
				class="mr-10 flex-shrink-0"
			>
				<img src="~/assets/logo1.svg" alt="Logo" class="h-8">	
			</nuxt-link>
			<a href="" @click.prevent="mobileNavOpen = !mobileNavOpen"
				class="lg:hidden ml-auto flex flex-col justify-center w-8 h-8" 
			>
				<span class="bg-blue-500 h-1 w-8 rounded mb-1"></span>
				<span class="bg-blue-500 h-1 w-8 rounded mb-1"></span>
				<span class="bg-blue-500 h-1 w-8 rounded mb-1"></span>
			</a>
			<div class="w-full flex"
				:class="{
					'mt-8': mobileNavOpen,
					'hidden lg:flex': !mobileNavOpen
				}"
			>
				<ul class="lg:flex items-center lg:h-24 w-full lg:w-auto">
					<li>
						<nuxt-link
							:to="{ name: 'browse' }"
							class="text-gray-700 text-lg lg:py-8 lg:px-4"
						>
							Browse
						</nuxt-link>
					</li>
					<li>
						<nuxt-link
							:to="{ name: 'search' }"
							class="text-gray-700 text-lg lg:py-8 lg:px-4"
						>
							Search
						</nuxt-link>
					</li>
				</ul>
				<ul class="lg:flex items-center lg:h-24 ml-auto text-right w-full lg:w-auto">
					<template v-if="$auth.loggedIn">
						<li>
							<nuxt-link
								:to="{ name: 'dashboard' }"
								class="text-gray-700 text-lg lg:py-8 lg:px-4"
							>
								Dashboard
							</nuxt-link>
						</li>
						<li>
							<nuxt-link
								:to="{ name: 'account' }"
								class="text-gray-700 text-lg lg:py-8 lg:px-4"							
							>
								{{ $auth.user.name }}
							</nuxt-link>
						</li>
						<li>
							<a
								href="#"
								@click.prevent="signOut"
								class="text-gray-700 text-lg lg:py-8 lg:px-4"
							>
								Sign Out
							</a>
						</li>
					</template>
					<template v-else>
						<li>
							<nuxt-link
								:to="{ name: 'auth-signin' }"
								class="text-gray-700 text-lg lg:py-8 lg:px-4"
							>
								Sign In
							</nuxt-link>
						</li>
						<li>
							<nuxt-link
								:to="{ name: 'auth-signup' }"
								class="text-gray-700 text-lg lg:py-8 lg:px-4"
							>
								Create an Account
							</nuxt-link>
							
						</li>
					</template>				
				</ul>
			</div>
		</div>
	</div>
</template>
<script type="text/javascript">
	export default {
		data () {
			return {
				mobileNavOpen: false
			}
		},
		methods: {
			async signOut () {
				await this.$auth.logout()
			}
		}
	}
</script>