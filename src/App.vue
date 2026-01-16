<script setup lang="ts">
import { computed, ref } from "vue";
import type { Task, TaskFilter } from "./types";
import ToDoForm from "./components/ToDoForm.vue";
import TodoList from "./components/TodoList.vue";
import FilterButton from "./components/FilterButton.vue";

const todos = ref<Task[]>([]);
const filter = ref<TaskFilter>("all");

const totalDone = computed(() =>
  todos.value.reduce((total, task) => (task.done ? total + 1 : total), 0)
);

const filteredTask = computed(() => {
  switch (filter.value) {
    case "all":
      return todos.value;
    case "done":
      return todos.value.filter((task) => task.done);
    case "todo":
      return todos.value.filter((task) => !task.done);
  }
  return todos.value;
});

function addTask(newTask: string) {
  todos.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    done: false,
  });
}

function toggleDone(id: string) {
  const task = todos.value.find((task) => task.id === id);

  if (task) {
    task.done = !task.done;
  }
}

function removeTask(id: string) {
  const index = todos.value.findIndex((task) => task.id === id);

  if (index != -1) {
    todos.value.splice(index, 1);
  }
}

function setFilter(value: TaskFilter) {
  filter.value = value;
}
</script>

<template>
  <main class="container">
    <div>
      <h1>ToDo App</h1>
      <ToDoForm @add-task="addTask" />
      <h3 v-if="!todos.length">Add your first Task to do.</h3>
      <h3 v-else>{{ totalDone }} / {{ todos.length }} tasks completed</h3>

      <div v-if="todos.length" class="filter-buttons">
        <FilterButton
          :currentFilter="filter"
          filter="all"
          @set-filter="setFilter"
        />
        <FilterButton
          :currentFilter="filter"
          filter="done"
          @set-filter="setFilter"
        />
        <FilterButton
          :currentFilter="filter"
          filter="todo"
          @set-filter="setFilter"
        />
      </div>
    </div>

    <TodoList
      :todos="filteredTask"
      @toggle-done="toggleDone"
      @remove-task="removeTask"
    />
  </main>
</template>

<style scoped>
.container {
  width: 800px;
  margin: 1rem auto;
  text-align: center;
  height: 100vh;
}

.filter-buttons {
  display: flex;
  justify-content: center;
  gap: 10px;
  margin-top: 10px;
}
</style>
