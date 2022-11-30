<template>
	
		
	<Form 
		ref="projectForm"
		@submit="submitProject"
		:validation-schema="projectFormSchema">

		<div class="card text-info bg-light">
			<div class="card-body">
				<div class="form-group">
					<label for="name">Tên truyện:</label>
					<Field
						name="name"
						type="text"
						class="form-control"
						v-model="projectLocal.name"
						placeholder="Nhập vào tên truyện"
					/>
					<ErrorMessage name="name" class="error-feedback" />
				</div>
				<div class="form-group">
					<label for="decripsion">Tóm tắt nội dung:</label>
					<textarea v-model="projectLocal.decripsion" class="form-control" placeholder="Nhập nội dung truyện"></textarea>

					<ErrorMessage name="decripsion" class="error-feedback" />
				</div>
				<div class="form-group">
					<label for="link">Đường dẫn:</label>
					<Field
						name="link"
						type="text"
						class="form-control"
						v-model="projectLocal.link"
						placeholder="Nhập đường dẫn truyện"
					/>
						<ErrorMessage name="link" class="error-feedback" />
				</div>
				<div class="form-group form-check">
						<input
							name="favorite"
							type="checkbox"
							class="form-check-input"
							v-model="projectLocal.favorite"
						/>
					<label for="favorite" class="form-check-label">
						<strong >Truyện yêu thích</strong>
					</label>
        		</div>
				<div class="form-group">
					<button class="btn btn-primary">
						<i class="fas fa-save"></i> Lưu
					</button>
					<button
						v-if="projectLocal._id"
						type="button"
						class="ml-2 btn btn-danger"
						@click="deleteProject"
					>
						<i class="fas fa-trash"></i> Xóa
					</button>
				</div>
			</div>
		</div>
	</Form>
		
	
</template>

<script>
import * as yup from "yup";
import { Form, Field, ErrorMessage } from "vee-validate";

export default {
	components: {
		Form,
		Field,
		ErrorMessage,
	},
	emits: ["submit:project", "delete:project"],
	props: {
		project: { type: Object, required: true },
		resetAfterSubmit: { type: Boolean, default: false },
	},
	data() {
		const projectFormSchema = yup.object().shape({
			name: yup
				.string()
				.required("Tên phải có giá trị.")
				.min(2, "Tên phải ít nhất 2 ký tự.")
				.max(50, "Tên có nhiều nhất 50 ký tự."),
		
			decripsion: yup.string().max(1000, "Mô tả tối đa 1000 ký tự."),
			link:yup.string(),
		
		});
		return {
			projectLocal: this.project,
			projectFormSchema,
		};
	},
	methods: {
		submitProject() {
			this.$emit("submit:project", this.projectLocal);
			if (this.resetAfterSubmit) {
				this.$refs.projectForm.resetForm();
			}
		},
		deleteProject() {
			this.$emit("delete:project", this.projectLocal._id);
		},
	},
};
</script>

<style scoped>
@import "@/assets/form.css";
</style>
