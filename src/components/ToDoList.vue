<template>
    <!-- Main component for To-Do List -->
    <div class="todo-list">
      <h1>To-Do List</h1>
  
      <!-- Add a new task section -->
      <div class="add-task">
        <!-- Input for new task -->
        <input v-model="newTaskText" @keyup.enter="addTask" placeholder="Add a new task" />
        <!-- Button to add task -->
        <button @click="addTask">Add</button>
        <!-- Additional input elements (Text, Checkbox, Radio, Select, Textarea) -->
        <input type="text" v-model="textInput" placeholder="Text Input" />
        <input type="checkbox" v-model="checkboxInput" />
        <input type="radio" v-model="radioInput" />
        <select v-model="selectInput">
          <option value="option1">Option 1</option>
          <option value="option2">Option 2</option>
        </select>
        <textarea v-model="textareaInput" placeholder="Textarea"></textarea>
      </div>
  
      <!-- Display tasks section -->
      <h2>List Rendering Examples:</h2>
  
      <div>
        <!-- b. v-model with checkboxes -->
        <h3>b. v-model with <input type="checkbox">:</h3>
        <ul>
          <!-- Iterate through tasks and bind checkboxes -->
          <li v-for="task in tasks" :key="task.id">
            <input type="checkbox" v-model="task.completed" />
            {{ task.text }}
          </li>
        </ul>
      </div>
  
      <div>
        <!-- c. v-for on <div> -->
        <h3>c. v-for on &lt;div&gt;:</h3>
        <ul>
          <li v-for="task in completedTasks" :key="task.id">
            {{ task.text }} (Completed)
          </li>
          <li v-for="task in incompleteTasks" :key="task.id">
            {{ task.text }} (Not Completed)
          </li>
        </ul>
      </div>
  
      <div>
        <!-- d. v-for with v-if -->
        <h3>d. v-for with v-if:</h3>
        <ul>
          <li v-for="task in completedTasks" :key="task.id">
            {{ task.text }}
          </li>
        </ul>
      </div>
  
      <div>
        <!-- e. v-for with a Component and Slots -->
        <h3>e. v-for with a Component and Slots:</h3>
        <ul>
          <!-- Use custom TaskItem component to render tasks -->
          <TaskItem
            v-for="task in tasks"
            :key="task.id"
            :task="task"
            @remove-task="removeTask(task)"
            :show-details="true"
          >
            <!-- Define slot for custom content within TaskItem -->
            <template #default="{ task }">
              <span>{{ task.text }}</span>
              <button @click="removeTask(task)">Remove</button>
            </template>
          </TaskItem>
        </ul>
      </div>
  
      <div>
        <!-- Display total tasks count -->
        <p>Total Tasks: {{ totalTasks }}</p>
      </div>
  
      <!-- Custom Content Slot -->
      <div class="custom-content">
        <slot name="custom-content"></slot>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, computed, watchEffect } from 'vue';
  import TaskItem from './TaskItem.vue';
  
  export default {
    components: {
      TaskItem,
    },
    setup() {
      const newTaskText = ref(''); // Input for new task text
      const tasks = ref([ // Array to store tasks
        { id: 1, text: 'Task 1', completed: false },
        { id: 2, text: 'Task 2', completed: true },
        { id: 3, text: 'Task 3', completed: false },
      ]);
      const textInput = ref(''); // Additional input fields
      const checkboxInput = ref(false);
      const radioInput = ref('');
      const selectInput = ref('option1');
      const textareaInput = ref('');
      const selectedRadio = ref('');
  
      // Function to add a new task
      const addTask = () => {
        if (newTaskText.value.trim() === '') return;
  
        tasks.value.push({
          id: tasks.value.length + 1,
          text: newTaskText.value,
          completed: false,
        });
  
        newTaskText.value = '';
      };
  
      // Computed properties for task filtering
      const completedTasks = computed(() => tasks.value.filter(task => task.completed));
      const incompleteTasks = computed(() => tasks.value.filter(task => !task.completed));
      const totalTasks = computed(() => tasks.value.length);
  
      // Function to remove a task
      const removeTask = taskToRemove => {
        tasks.value = tasks.value.filter(task => task !== taskToRemove);
      };
  
      // Watcher to keep selected radio value in sync
      watchEffect(() => {
        selectedRadio.value = radioInput.value;
      });
  
      return {
        newTaskText,
        tasks,
        textInput,
        checkboxInput,
        radioInput,
        selectInput,
        textareaInput,
        selectedRadio,
        addTask,
        completedTasks,
        incompleteTasks,
        totalTasks,
        removeTask,
      };
    },
  };
  </script>
  
  <style scoped>
  .todo-list {
    font-family: Arial, sans-serif;
    max-width: 600px;
    margin: 0 auto;
    padding: 20px;
    background-color: #f8f8f8;
    border: 1px solid #ccc;
    border-radius: 8px;
  }
  
  .add-task {
    display: flex;
    margin-top: 20px;
  }
  
  .add-task input[type="text"] {
    flex-grow: 1;
    padding: 10px;
    margin-right: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
    width: 100%; /* Make the text input 100% width */
  }
  
  .add-task select,
  .add-task textarea {
    flex-grow: 1;
    padding: 10px;
    margin-right: 10px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }
  
  .add-task button {
    padding: 10px 16px;
    background-color: #007BFF;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
  }
  
  ul {
    list-style: none;
    padding: 0;
  }
  
  li {
    margin: 10px 0;
    display: flex;
    align-items: center;
  }
  
  input[type="checkbox"] {
    margin-right: 10px;
  }
  
  button {
    background-color: #DC3545;
  }
  
  .custom-content {
    margin-top: 20px;
    border: 1px solid #ccc;
    padding: 10px;
    background-color: white;
  }
  </style>
  