<template>
    <div class="task-item">
      <input type="checkbox" v-model="completed" @change="onCompleteChange" />
      <span>{{ task.text }}</span>
      <button @click="removeTask">Remove</button>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      task: {
        type: Object,
        required: true
      }
    },
    computed: {
      completed: {
        get() {
          return this.task.completed;
        },
        set(value) {
          this.$emit('complete-change', value);
        }
      }
    },
    methods: {
      onCompleteChange(event) {
        this.completed = event.target.checked;
      },
      removeTask() {
        this.$emit('remove-task', this.task);
      }
    }
  };
  </script>
  
  <style scoped>
  .task-item {
    display: flex;
    align-items: center;
    margin-bottom: 5px;
  }
  
  input[type="checkbox"] {
    margin-right: 10px;
  }
  </style>
  