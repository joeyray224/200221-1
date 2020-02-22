<template>
  <form class="new-task" @submit.prevent="createTask">
    <input class="new-task__item" type="text" placeholder="*Название" v-model="name">
    <textarea class="new-task__item" rows="5" placeholder="*Описание"
      v-model="description"></textarea>
    <button class="new-task__btn"
      :title="title"
      :disabled="!name.trim().length || !description.trim().length"
      @mouseover="overCreate"
    >
      Создать
    </button>
  </form>
</template>

<script>
export default {
	name: 'create-task',
	props: {
		items: {
			type: Array,
			required: true,
		},
	},
	data() {
		return {
			name: '',
			description: '',
			title: 'Заполните обязательные поля',
		};
	},
	methods: {
		createTask() {
			this.$emit('create-task', {
				id: this.getUniqueNumber,
				name: this.name,
				description: this.description,
				flag: false,
			});

			this.name = '';
			this.description = '';
			this.title = 'Заполните обязательные поля';
		},
		overCreate() {
			this.title = '';
		},
	},
	computed: {
		getUniqueNumber() {
			return this.items.length ? Math.max.apply(null, this.items.map((e) => e.id)) + 1 : 1;
		},
	},
};
</script>

<style lang="scss" scoped>
  .new-task {
    width: 60%;
    margin: auto;
    display: flex;
    flex-direction: column;

    &__item {
      font-family: 'Courier New', Courier, monospace;
      font-size: 18px;
      margin: 3px;
      padding: 10px;
      border: 2px solid #999;
      border-radius: 10px;
      outline: unset;
      &:nth-child(2) {
        resize: unset;
      }
    }
    &__btn {
      width: 150px;
      padding: 10px;
      border-radius: 10px;
      font-size: 20px;
      color: #fff;
      background: #444;
      border: none;
      margin: 10px auto;
      transition: .8s ease;
      &:hover {
        cursor: pointer;
        background: #777;
      }
      &:disabled {
        cursor: unset;
        background: #cdcdcd;
      }
    }
  }
</style>>
