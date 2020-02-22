<template>
	<div class="task-del">
		<button class="task-del__btn"
			@click="removeTask"
			:disabled="!getLengthList"
		>Удалить</button>
	</div>
</template>

<script>
export default {
	name: 'remove-task',
	props: {
		items: {
			type: Array,
			required: true,
		},
		getLengthList: {
			type: Number,
			required: true,
		},
	},
	data() {
		return {

		};
	},
	methods: {
		removeTask() {
			this.$emit('remove-task', this.getCheckedItems);
		},
	},
	computed: {
		getCheckedItems() {
			return this.items.filter((e) => !e.flag);
		},
	},
};
</script>

<style lang="scss" scoped>
  .task-del {
    display: flex;
    justify-content: flex-start;
		&__btn {
      width: 100px;
      padding: 10px;
      border-radius: 10px;
      font-size: 20px;
      color: #fff;
      background: #ad5959;
      border: none;
      margin: 10px;
			outline: none;
      transition: .8s ease;
			&:hover {
				cursor: pointer;
				background: #cc7c7c;
			}
			&:disabled {
				cursor: unset;
				background: #e2b5b5;
			}
    }
  }
</style>>
