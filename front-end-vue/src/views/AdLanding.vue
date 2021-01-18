<template>
	<v-app>
		<v-content>
			<v-card class="mx-auto overflow-hidden">
				<v-app-bar>
					<v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

					<!-- <v-toolbar-title>GLUG AUDITIONS 2020</v-toolbar-title> -->
					<v-spacer></v-spacer><v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>
					<v-spacer></v-spacer>

					<v-btn @click="logout" color="#00FFFF">Logout</v-btn>
					<v-spacer></v-spacer>
					<!-- <v-btn @click="purge" color="light-blue darken-1">PURGE</v-btn> -->
				</v-app-bar>
			</v-card>

			<v-navigation-drawer v-model="drawer" absolute temporary>
				<v-list nav dense>
					<v-list-item-group
						v-model="group"
						active-class="deep-purple--text text--lighten-2"
					>
						<router-link tag="span" to="/">
							<v-list-item>
								<v-list-item-icon>
									<v-icon>mdi-home</v-icon>
								</v-list-item-icon>
								<v-list-item-title>Home</v-list-item-title>
							</v-list-item>
						</router-link>
						<v-list-item>
							<v-switch v-model="darkmode" label="Dark Mode"></v-switch>
						</v-list-item>
					</v-list-item-group>
				</v-list>
			</v-navigation-drawer>

			<v-container fluid>
				<div>
					<v-spacer>
            <v-alert
      outlined
      color="#00FFFF"
    >
     <h1 class="text-center">STUDENTS DASHBOARD</h1>
     
    </v-alert>
					</v-spacer>
				</div>
				<v-spacer />
				<v-spacer />
				<v-container absolute fluid>
					<v-row align="center" justify="center">
						<v-col cols="12" sm="6" lg="3">
							<v-alert outlined color="#00FFFF">
								<v-list-item three-line>
									<v-list-item-content>
										<div class="subtitle-2">TOTAL STUDENTS</div>
										<v-list-item-title class="display-2">{{
											items.length
										}}</v-list-item-title>
									</v-list-item-content>

									<v-list-item-avatar tile size="90">
										<v-img src="../assets/img/stu.png"></v-img>
									</v-list-item-avatar>
								</v-list-item>
							</v-alert>
						</v-col>
						<v-col cols="12" sm="6" lg="3">
								<v-alert outlined color="success">
								<v-list-item three-line>
									<v-list-item-content>
										<div class="subtitle-2">COMPLETED</div>
										<v-list-item-title class="display-2"></v-list-item-title>
										<v-list-item-subtitle></v-list-item-subtitle>
									</v-list-item-content>

									<v-list-item-avatar tile size="90">
										<v-img src="../assets/img/t.png"></v-img>
									</v-list-item-avatar>
								</v-list-item>
								</v-alert>
						</v-col>
						<v-col cols="12" sm="6" lg="3">
								<v-alert outlined color="warning">
								<v-list-item three-line>
									<v-list-item-content>
										<div class="subtitle-2">PENDING</div>
										<v-list-item-title class="display-2"></v-list-item-title>
									</v-list-item-content>

									<v-list-item-avatar tile size="90">
										<v-img src="../assets/img/w.png"></v-img>
									</v-list-item-avatar>
								</v-list-item>
								</v-alert>
						</v-col>
					</v-row>
				</v-container>

				<!-- <v-data-table
					:headers="headers"
					hide-default-footer
					:items="items"
					class="elevation-1"
				>
					<template v-slot:item="row">
						<tr @click="usercontrol(row.item)">
							<td>{{ row.item.name }}</td>
							<td>{{ row.item.selected.status }}</td>
							<td>{{ row.item.final.status }}</td>
							<td>{{ row.item.lastUser }}</td>
							<td>{{ row.item.selected.user }}</td>
							<td>
								<v-btn class="mx-2" light small @click="usercontrol(row.item)"
									>Detail</v-btn
								>
							</td>
						</tr>
					</template>
				</v-data-table> -->
				<template>
					<v-card>
						<v-tabs
							v-model="tab"
							color="cyan"
							
							dark
							icons-and-text
						>
							<v-tabs-slider></v-tabs-slider>

							<v-tab href="#subscribe">
								ROUND 1
							
							</v-tab>

							<v-tab href="#contact">
								ROUND 2
								
							</v-tab>
						</v-tabs>

						<v-tabs-items v-model="tab">
							<v-tab-item :key="1" value="subscribe">
								<v-data-table
									:headers="headers"
									hide-default-footer
									:items="items"
									class="elevation-1"
								>
									<template v-slot:item="row">
										<tr @click="usercontrol(row.item)">
											<td>{{ row.item.name }}</td>
											<td>{{ row.item.selected.status }}</td>
											<td>{{ row.item.final.status }}</td>
											<td>{{ row.item.lastUser }}</td>
											<td>{{ row.item.selected.user }}</td>
											<td>
												<v-btn class="mx-2" light small @click="usercontrol(row.item)"
													>Detail</v-btn
												>
											</td>
										</tr>
									</template>
								</v-data-table>
							</v-tab-item>
							<v-tab-item :key="2" value="contact">
								<v-card flat>
									<v-card-text>contact</v-card-text>
								</v-card>
							</v-tab-item>
						</v-tabs-items>
					</v-card>
				</template>
			</v-container>
		</v-content>
	</v-app>
</template>

<script>
import common from "@/services/common.js";
export default {
	name: "Landing",
	components: {},

	data() {
		return {
			drawer: false,
			adminUser: localStorage.getItem("admin"),
			items: [],
			expand: false,
			darkmode: false,
			headers: [
				{ text: "FULL NAME", align: "start", value: "name" },
				{ text: "STATUS", align: "start", value: "status" },
				{ text: "FINAL STATUS", align: "start", value: "final status" },
				{ text: "LAST VIEWED", align: "start", value: "details" },
				{ text: "LAST CHANGED", align: "start", value: "details" },
				{ text: "DETAILS", align: "start", value: "details" }
			],
			tab: null,
			rounds: ["web", "shopping", "videos", "images", "news"]
		};
	},
	watch: {
		darkmode(newvalue) {
			this.$vuetify.theme.dark = newvalue;
		}
	},
	created() {
		if (localStorage.getItem("token") === null) {
			localStorage.clear();
			this.$router.push("/");
		} else {
			common.getUsers().then(res => {
				if (res.status === 200) {
					this.items = res.data.doc;
				} else if (res.status === 401) {
					alert("UNAUTHORISED ACCESS");
					localStorage.clear("token");
					this.$router.push("/");
				} else {
					alert("No data");
				}
			});
		}
		this.$vuetify.theme.dark = true;
	},
	methods: {
		logout() {
			common.logout().then(res => {
				localStorage.clear();
				alert(res.data);
				this.$router.push("/AdLog");
			});
		},
		usercontrol(a) {
			var payload = a;
			payload["lastUser"] = this.adminUser;
			common.updateEntry(payload);
			let routeData = this.$router.resolve({
				name: "UserControl",
				query: { id: a._id }
			});
			window.open(routeData.href, "_blank");
		},
		purge() {
			common.purge().then(res => {
				alert(res.data.message);
				location.reload();
			});
		}
	}
};
</script>
