<script setup lang="ts">
import type { Task } from "../types";

const props = defineProps<{
  todos: Task[];
}>();

const emits = defineEmits<{
  toggleDone: [id: string];
  removeTask: [id: string];
}>();
</script>

<template>
  <div class="todo-list">
    <div class="list-container" v-for="task in $props.todos" :key="task.id">
      <label class="task">
        <input
          @input="emits('toggleDone', task.id)"
          :checked="task.done"
          type="checkbox"
        />
        <span :class="{ done: task.done }">{{ task.title }}</span>
      </label>
      <button @click="emits('removeTask', task.id)">Remove</button>
    </div>
  </div>
</template>

<style scoped>
.list-container {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.task {
  width: 550px;
  display: flex;
  align-items: center;
  gap: 1rem;
  padding: 6px 3px;
  cursor: pointer;
  background-color: rgba(50, 250, 50, 0.2);
  font-size: 1.5rem;
  margin: 10px;
}
input {
  width: 30px;
  height: 30px;
  margin-left: 10px;
}

.done {
  text-decoration: line-through;
}

button {
  background-color: #555;
  color: #ddd;
  border: 1px solid #ddd;
  cursor: pointer;
}

button:hover {
  background-color: green;
  border-style: none;
}
</style>
