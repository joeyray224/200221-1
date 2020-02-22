<template>
  <div class="task">
    <h1 class="task__title">{{ msg }}</h1>

    <TaskList
      :items="items"
      :isLoad="isLoad"
      @create-task="createTask"
      @filter-task="filterTask"
      @remove-task="removeTask"
    />

  </div>
</template>

<script>
import TaskList from '@/components/childs/TaskList.vue';

export default {
	name: 'Task',
	props: {
		msg: String,
	},
	components: {
		TaskList,
	},
	data() {
		return {
			isLoad: true,
			items: [
				{
					id: 1,
					name: 'Первая задача',
					description: 'Lorem ipsum dolor sit amet consectetur adipisicing elit. Ea, veniam.',
					flag: true,
				},
				{
					id: 2,
					name: 'Вторая задача',
					description: 'Lorem ipsum dolor sit, amet consectetur adipisicing elit. Exercitationem commodi architecto velit libero dolor officia unde, cum corporis est dolorum?',
					flag: false,
				},
			],
		};
	},
	methods: {
		createTask(data) {
			this.items.push(data);
		},
		removeTask(data) {
			this.items = data;
		},
		filterTask(data) {
			this.items = data;
		},
	},
	mounted() {
		const loading = new Promise((resolve) => {
			setTimeout(() => {
				resolve(false);
			}, 3000);
		});
		loading
			.then((data) => { this.isLoad = data; });
	},
};
</script>

<style scoped lang="scss">
  .task {
    margin: auto;
    padding: 15px;
    box-shadow: 0 0 100px 10px #444;
    &__title {
      text-align: center;
    }
  }
</style>
