<template>
	
	<nav class="navbar navbar-expand navbar-dark btn btn-info">
		<a href="/" class="navbar-brand">Quản lý truyện </a>


		<div v-if="!currentUser" class="navbar-nav ml-auto">
			<li class="nav-item">
				<router-link :to="{ name: 'login' }" class="nav-link"
					>Đăng nhập</router-link
				>
			</li>
			<li class="nav-item">
				<router-link :to="{ name: 'register' }" class="nav-link"
					>Đăng ký</router-link
				>
			</li>
			
		</div>

		<div v-if="currentUser" class="navbar-nav ml-auto">
			<li class="nav-item">
				<router-link :to="{ name: 'profile' }" class="nav-link"><span>Xin chào,  </span>{{
					currentUser.username
				}}</router-link>
			</li>
			<li class="nav-item">
				<a class="nav-link" @click.prevent="handleLogout">Đăng xuất</a>
			</li>
		</div>
	</nav>

</template>

<script>
import { mapState, mapActions } from "pinia";
import { useAuthStore } from "@/stores/auth.store";

export default {
	computed: {
		...mapState(useAuthStore, {
			currentUser: "user",
		}),
	},
	methods: {
		...mapActions(useAuthStore, ["logout", "loadAuthState"]),

		handleLogout() {
			this.logout();
			this.$router.push({ name: "login" });
		},
	},
	created() {
		this.loadAuthState();
	},
};
</script>
