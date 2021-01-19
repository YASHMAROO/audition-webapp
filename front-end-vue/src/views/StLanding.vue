<template>
	<div id="app">
		<span class="bg"></span>
		<v-app id="inspire">
			<v-content>
				<v-card class="mx-auto overflow-hidden" color="#121a26">
					<v-app-bar color="#141d2b" fixed>
						<v-btn @click="logout" color="#B2EBF2"><span style="color: #000 !important;">Logout</span></v-btn>
					</v-app-bar>
				</v-card>
				<v-container fluid class="question_cont">
					<Normalques />
					<Test />
				</v-container>	
			</v-content>
		</v-app>
	</div>
</template>

<script>
import common from "@/services/common.js";
import Normalques from "../components/Normalques";
import Test from "../components/Test";

import axios from "axios";
export default {
	components: {
		Normalques,
		Test
	},
	name: "Landing",
	beforeCreate() {
		if (localStorage.getItem("token") === null) {
			this.$router.push("/");
		} else {
			axios.get().then(res => {
				console.log(res.data);
				if (res.data.isAdmin === false) {
					console.log(res.data);
				} else {
					alert("You are the Admin. Accessing wrong route, re-routing");
					this.$router.push("/AdLog");
				}
			});
		}
	},
	created() {
		this.$vuetify.theme.dark = true;
	},
	methods: {
		logout() {
			common.logout().then(res => {
				alert(res.data);
				this.$router.push("/StLog");
			});
		}
	}
};
</script>

<style scoped>
.bg {
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	left: 0;
	background-size: cover;
	background-color: #141d2b;
	opacity: 0.4;
}

.question_cont {
	margin-top: 5rem !important;
}

@media only screen and (max-width: 576px) {
	.question_cont {
		margin-top: 3rem !important;
	}
}
</style>
