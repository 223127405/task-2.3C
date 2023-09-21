<template>
  <div id="app">
    <router-view></router-view>
    <ToDoList />
    <TaskItem />
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue';
import TaskItem from './components/TaskItem.vue';

export default {
  name: 'App',
  components: {
    ToDoList,
    TaskItem
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
