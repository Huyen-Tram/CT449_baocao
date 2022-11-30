<script>
export default {
	props: {
		project: { type: Object, required: true },
	},
	el: '#container',

  methods: {
    copy() {
      try {
        navigator.clipboard.writeText(this.project.link);
		alert('Bạn đã copy thành công link phim '+ this.project.name);
      } catch (e) {
        throw e
      }
    }
  },
};

</script>

<template>
	<div class="card text-white bg-info">
		<div class="card-body">
  
			<div class="p-1">
				<strong class="card-text text-warning">Tên truyện:</strong>
				{{ project.name }}
			</div>
			<div class="p-1">
				<strong class="card-text text-warning"> Tóm tắt nội dung:</strong>
				{{ project.decripsion }}
			</div>
			<div class="p-1">
				<strong class="card-text text-warning">Đường dẫn:</strong><br>
				{{ project.link }} 

				
			</div>
	
			<div class="p-1">
				<strong class="card-text text-warning">Truyện yêu thích:&nbsp;</strong>
				<i v-if="project.favorite" class="fas fa-check"></i>
				<i v-else class="fas fa-times"></i>
			</div>
			
			
		</div>
	</div>
</template>
