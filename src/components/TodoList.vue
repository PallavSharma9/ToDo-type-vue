<script setup lang="ts">
import type { Task } from "../types";

const props = defineProps<{
  todos: Task[];
}>();
</script>

<template>
  <div class="todo-list">
    <div v-for="task in $props.todos">
      <label class="task">
        <input type="checkbox" />
        <span>{{ task.title }}</span>
      </label>
    </div>
  </div>
</template>

<style scoped>
.task {
  width: 600px;
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 6px 3px;
  cursor: pointer;
  background-color: rgba(50, 250, 50, 0.2);
  font-size: 1.5rem;
  margin: 10px auto;
}
input {
  width: 30px;
  height: 30px;
  margin-left: 10px;
}
</style>
