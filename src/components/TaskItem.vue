<script setup>
// Props define the task object and functions to toggle completion and delete the task
defineProps({
  task: Object,
  toggleComplete: Function,
  deleteTask: Function
});
</script>

<template>
  <li>
    <!-- Checkbox to mark task complete/incomplete -->
    <input type="checkbox" :checked="task.completed" @change="toggleComplete(task.id)" />
    <!-- Task text, styled with line-through if completed -->
    <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.text }}</span>
    <!-- Button to delete the task -->
    <button @click="deleteTask(task.id)">Delete</button>
  </li>
</template>

<style scoped>
li {
  list-style: none;
  margin: 0.5em 0;
  display: flex;
  align-items: center;
}
span {
  flex-grow: 1;
  margin-left: 0.5em;
}
button {
  margin-left: 1em;
  background-color: #ff4d4d;
  border: none;
  color: white;
  padding: 0.2em 0.5em;
  cursor: pointer;
  border-radius: 3px;
}
button:hover {
  background-color: #ff1a1a;
}
</style>
