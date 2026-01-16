<script setup lang="ts">
import { ref } from "vue";
import type { Task } from "./types";
import ToDoForm from "./components/ToDoForm.vue";
import TodoList from "./components/TodoList.vue";

const todos = ref<Task[]>([]);

function addTask(newTask: string) {
  todos.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
}
</script>

<template>
  <main class="container">
    <div>
      <h1>ToDo App</h1>
      <ToDoForm @add-task="addTask" />
      <h3 v-if="!todos.length">Add your first Task to do.</h3>
      <h3 v-else>0 / {{ todos.length }} tasks completed</h3>
    </div>

    <TodoList :todos />
  </main>
</template>

<style scoped>
.container {
  width: 800px;
  margin: 1rem auto;
  text-align: center;
  height: 100vh;
}
</style>
