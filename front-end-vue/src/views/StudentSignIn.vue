<template>
	<v-app id="inspire">
		<v-content>
			<Sidenav />

			<Particle />

			<v-container fluid class="centered">
				<v-row align="center" justify="center">
					<v-col cols="12" sm="8" md="4">
						<v-card class="elevation-12">
							<v-toolbar color="" dark flat>
								<v-spacer></v-spacer>
								<v-toolbar-title> STUDENT LOGIN </v-toolbar-title>
								<v-spacer />
							</v-toolbar>
							<v-card-text>
								<v-form>
									<v-text-field
										v-model="email"
										label="Email"
										name="login"
										prepend-icon="person"
										type="text"
									/>

									<v-text-field
										v-model="password"
										id="password"
										label="Password"
										name="password"
										prepend-icon="lock"
										type="password"
									/>
								</v-form>
							</v-card-text>
							<v-divider></v-divider>
							<v-card-actions>
								

								<v-container align="center">
									<v-row align="center" justify="center">
										<v-col cols="12">
											<v-btn @click="send" color="lime accent-4"  block>Login</v-btn>
										</v-col>
									</v-row>
									<v-row align="center" justify="center">
										<v-col cols="6">
											<v-btn @click="goauth" color="red darken-2"  block>
												<v-img dark left src="https://upload-icon.s3.us-east-2.amazonaws.com/uploads/icons/png/357916981530077752-512.png" max-height="30" max-width="30"></v-img> LOGIN  
											</v-btn>
										</v-col>
										<v-col cols="6">
											<v-btn @click="fboauth" color="blue accent-4"  block>
												<v-img dark left src="https://1000logos.net/wp-content/uploads/2016/11/Facebook-logo.png" max-height="50" max-width="50"></v-img> LOGIN 
											</v-btn>
										</v-col>
										<v-spacer/>
										<p class="subtitle-1" align="center">Don't have account  <a @click="$router.push('/StSign')">Register</a></p>
									</v-row>
								</v-container>
							</v-card-actions>
						</v-card>
					</v-col>
				</v-row>
			</v-container>
		</v-content>
	</v-app>
</template>

<script>
import common from '@/services/common.js'
import Particle from "../components/layout/Particle";
import Sidenav from "../components/layout/Sidenav";

export default {
	components: {
		Particle,
		Sidenav
	},
	data: () => ({
		drawer: false,
		email: "",
		password: ""
	}),
	props: {
		source: String
	},
	created() {
		localStorage.clear();
		this.$vuetify.theme.dark = true;
	},
	methods: {
		send() {
			var user = {
				email: this.email,
				password: this.password
			};
			common.login(user).then(res => {
				if (res.data.success == true) {
					localStorage.setItem("token", res.data.token);
					alert("Successful login");
					this.$router.push("/Stlanding");
				} else {
					alert(res.data.message);
					this.$router.push("/");
				}
			});
			
		},
		goauth() {
			window.location.href = `${process.env.VUE_APP_BASE_URL}/auth/google/`;
		},
		fboauth() {
			window.location.href = `${process.env.VUE_APP_BASE_URL}/auth/facebook/`;
		}
	}
};
</script>

<style scoped>
.centered {
	color: #ffffff;
	position: absolute;
	text-align: center;
	top: 20%;
	width: 100%;

}
</style>
