<template>
	<div v-if="currentUser">
		<header class="jumbotron bg-info">
			<h3>
				<span class="text-black"> Xin chào </span>
				<strong class="text-warning">  {{ currentUser.username }}</strong>
				<br>
				<br>
				<span class="text-white" style="font-style: italic; font-size: large;"> Đây là các thông tin của bạn</span> 
				<br>
				
			</h3>
			<div class="col-md-8">
				
				<p>
					<strong>Id:</strong>
					{{ currentUser._id }}
				</p>
				<p>
					<strong>E-mail:</strong>
					{{ currentUser.email }}
				</p>
			</div>
		</header>
	</div>
</template>

<script>
import { mapState } from "pinia";
import { useAuthStore } from "@/stores/auth.store";

export default {
	computed: {
		...mapState(useAuthStore, {
			currentUser: "user",
		}),
	},
	created() {
		if (!this.currentUser) {
			this.$router.push({ name: "login" });
		}
	},
};
</script>
