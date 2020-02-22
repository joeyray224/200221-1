<template>
	<div>
		<!-- Create Task -->
		<CreateTask
      :items="items"
			:getLengthList="getLengthList"
      @create-task="createTask"
    />
		<template v-if="isLoad">
      <div class="shadow">
        <span class="shadow__loader">Loading...</span>
      </div>
    </template>
    <template v-else>
			<div class="filter-container">
				<!-- Filter Task -->
				<FilterTask
					:items="items"
					@filter-task="filterTask"
				/>
				<!-- Search Task -->
				<SearchTask
					:items="items"
					@search-task="searchTask"
				/>
			</div>
      <div class="task-list">
        <div class="task-list__title-list">
          <div class="task-list__title-item task-list__title-item--checked">Выбрать задачу</div>
          <div class="task-list__title-item task-list__title-item--number">Порядковый номер</div>
          <div class="task-list__title-item task-list__title-item--task">Название задачи</div>
          <div class="task-list__title-item task-list__title-item--desc">Описание задачи</div>
        </div>
        <div v-if="getLengthList > 0" class="task-list__item-box">
          <div class="task-list__item-list"
              v-for="item of searchItems"
              :key="item.id"
              >
            <div class="task-list__item task-list__item--checked">
              <input class="task-list__item-checkbox" type="checkbox" v-model="item.flag">
            </div>
            <div class="task-list__item task-list__item--number">
              {{ item.id }}
            </div>
            <div class="task-list__item task-list__item--task">
              {{ item.name }}
            </div>
            <div class="task-list__item task-list__item--desc">
              {{ item.description }}
            </div>
          </div>
        </div>
				<div v-else class="task-list__item-info">
					Список пуст
				</div>
      </div>
			<!-- Remove Task -->
			<RemoveTask
				:items="items"
				:getLengthList="getLengthList"
				@remove-task="removeTask"
			/>
    </template>
	</div>
</template>

<script>
import CreateTask from '@/components/childs/handles/CreateTask.vue';
import FilterTask from '@/components/childs/handles/FilterTask.vue';
import RemoveTask from '@/components/childs/handles/RemoveTask.vue';
import SearchTask from '@/components/childs/handles/SearchTask.vue';

export default {
	name: 'task-list',
	components: {
		CreateTask,
		FilterTask,
		RemoveTask,
		SearchTask,
	},
	props: {
		isLoad: {
			type: Boolean,
			required: true,
		},
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
	computed: {
		getLengthList() {
			return this.items.length;
		},
		searchItems() {
			return this.items.filter((e) => {
				const isName = e.name.toLowerCase().match(this.search);
				const isDesc = e.description.toLowerCase().match(this.search);
				return isName || isDesc;
			});
		},
	},
	methods: {
		createTask(data) {
			this.$emit('create-task', data);
		},
		removeTask(data) {
			this.$emit('remove-task', data);
		},
		filterTask(data) {
			this.$emit('filter-task', data);
		},
		searchTask(data) {
			this.search = data;
		},
	},
};
</script>

<style lang="scss" scoped>
	.filter-container {
		display: flex;
		justify-content: space-between;
	}
	.shadow {
    text-align: center;
    &__loader {
      font-size: 18px;
      font-weight: 700;
    }
  }
	.task-list {
    width: 700px;
    margin: auto;
    border: 1px solid #cdcdcd;
    &__title-list {
      display: flex;
    }
    &__title-item {
      padding: 10px;
      background: #444;
      color: #fff;
      font-weight: 700;
      display: flex;
      justify-content: center;
      align-items: center;
    }
		&__item-checkbox {
			width: 17px;
			height: 17px;
		}
		&__item-info {
			text-align: center;
			padding: 10px 0;
		}
    &__title-item--checked, &__item--checked,
    &__title-item--number, &__item--number {
      flex: 0 1 120px;
      text-align: center;
    }
    &__title-item--task, &__item--task,
    &__title-item--desc, &__item--desc {
      flex: 1 1 230px;
      text-align: center;
    }
    &__item-list {
      display: flex;
      &:nth-child(odd) {
        background: #acacac;
      }
    }
    &__item {
      padding: 5px 10px;
    }
  }
</style>>
