<template>
  <div class="about">
    <h1>Welcome to my about page</h1>
    
    <!-- Add a "Home" button to navigate back -->
    <router-link to="/">Home</router-link>
  </div>
</template>

<script>
export default {
  name: 'AboutView',
};
</script>

<style scoped>
/* Add styles specific to the AboutView component */
.about {
  text-align: center;
  padding: 20px;
}
</style> 