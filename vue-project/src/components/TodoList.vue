<script setup>
import { ref } from "vue";

const newTask = ref("");
const allTasks = ref([]);

const addTask = () => {
  if (newTask.value.trim() != "") {
    allTasks.value.push(newTask.value);
    newTask.value = "";
  }
};

const removeTask = (index) => {
  allTasks.value.splice(index, 1);
};
</script>

<template>
  <div class="todo-app">
    <div class="task-input">
      <input
        v-model="newTask"
        @keyup.ente="addTask"
        placeholder="add new task"
      />
      <button @click="addTask">Add New Task</button>
    </div>

    <ul class="task-list">
      <li v-for="(task, index) in allTasks" :key="index" class="task-item">
        {{ task }}
        <button @click="removeTask(index)" class="remove-button">
          Remove Task
        </button>
      </li>
    </ul>
  </div>
</template>
