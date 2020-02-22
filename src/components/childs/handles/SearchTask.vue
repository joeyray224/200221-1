<template>
	<div class="search-task">
		<input class="search-task__field" type="text" placeholder="Поиск"
			v-model="search"
			@input="searchTask"
		>
	</div>
</template>

<script>
export default {
	name: 'search-task',
	props: {
		items: {
			type: Array,
			required: true,
		},
	},
	data() {
		return {
			search: '',
		};
	},
	methods: {
		searchTask() {
			this.$emit('search-task', this.search.toLowerCase());
		},
	},
};
</script>

<style lang="scss" scoped>
	.search-task {
		flex: 0 1 100%;
		display: flex;
		justify-content: center;
		align-items: center;
		&__field {
			width: 100%;
      padding: 10px 20px;
      border-radius: 10px;
      font-size: 20px;
      color: #000;
      box-shadow: inset 0 0 20px 0 #444;
      border: none;
      margin: 10px;
			outline: none;
      transition: .8s ease;
		}
	}
</style>
