<template>
	<div class="filter-task">
		<button class="filter-task__btn"
			:class="{'filter-task__btn--active': isFilter}"
			@click="filterTask"
		>Фильтр</button>
	</div>
</template>

<script>
export default {
	name: 'filter-task',
	props: {
		items: {
			type: Array,
			required: true,
		},
	},
	data() {
		return {
			isFilter: false,
		};
	},
	computed: {
		getFilterItems() {
			if (this.isFilter) {
				return this.items
					.map((e) => e)
					.sort((a, b) => (a.name.toUpperCase() > b.name.toUpperCase() ? 1 : -1));
			}

			return this.items
				.map((e) => e)
				.sort((a, b) => a.id - b.id);
		},
	},
	methods: {
		filterTask() {
			this.isFilter = !this.isFilter;
			this.$emit('filter-task', this.getFilterItems);
		},
	},
};
</script>

<style lang="scss" scoped>
	.filter-task {
		flex: 0 1 110px;
		display: flex;
		justify-content: center;
		align-items: center;
		&__btn {
			width: 100%;
      padding: 10px;
      border-radius: 10px;
      font-size: 20px;
      color: #fff;
      background: #646ea0;
			background: linear-gradient(180deg, #646ea0, #181f54);
      border: none;
      margin: 10px;
			outline: none;
      transition: .8s ease;
			&:hover {
				cursor: pointer;
			}
			&--active {
				background: linear-gradient(180deg, #181f54, #646ea0);
			}
    }
	}
</style>
