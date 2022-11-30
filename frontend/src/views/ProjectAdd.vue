<template>
	<div class="page bg-white">
		<div>
			<h4 class="card-header bg-info text-white">Thêm truyện mới</h4>
			<ProjectForm
				:project="{}"
				:resetAfterSubmit="false"
				@submit:project="saveProject"
			/>
		</div>
	</div>
</template>

<script>
import { swtoast } from "@/mixins/swal.mixin";
import ProjectForm from "@/components/ProjectForm.vue";
import ProjectService from "@/services/project.service";

export default {
	components: {
		ProjectForm,
	},
	methods: {
		async saveProject(data) {
			try {
				await ProjectService.create(data);
					this.$router.push({ name: "project" });
			} catch (error) {
				console.log(error);
			}		
		},
	},
};
</script>
