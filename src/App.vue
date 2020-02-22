<template>
  <div id="app">
    <Task msg="Создание списка задач"/>
  </div>
</template>

<script>
import Task from './components/Task.vue';

export default {
	name: 'App',
	components: {
		Task,
	},
};
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Exo+2:400,700&display=swap');
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  #app {
    max-width: 800px;
    height: calc(100vh - 16px);
    font-family: 'Exo 2', sans-serif;
    margin: auto;
    display: flex;
    flex-direction: column;
  }
</style>
