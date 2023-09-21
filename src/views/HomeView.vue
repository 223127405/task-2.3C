<template>
  <div class="home">
    <h1>Welcome to the To-Do List</h1>

    <router-link to="/">Home</router-link>
    <router-link to="/about">About</router-link>

    <ToDoList>
      <template #custom-content>
        <p>This is original content that has been added to the To-Do List feature.</p>
      </template>
    </ToDoList>
  </div>
</template>


<script>
import ToDoList from '@/components/ToDoList.vue';

export default {
  name: 'HomeView',
  components: {
    ToDoList,
  },
};
</script>

<style scoped>
/* Add styles specific to the HomeView component */
.home {
  text-align: center;
  padding: 20px;
}
</style> 