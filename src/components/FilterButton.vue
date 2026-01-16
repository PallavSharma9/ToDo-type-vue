<script lang="ts" setup>
import type { TaskFilter } from "../types";

const props = defineProps<{
  filter: TaskFilter;
  currentFilter: TaskFilter;
}>();

const emits = defineEmits<{
  setFilter: [filter: TaskFilter];
}>();
</script>

<template>
  <button
    @click="emits('setFilter', props.filter)"
    :class="{ contrast: $props.currentFilter === props.filter }"
  >
    {{ props.filter }}
  </button>
</template>

<style scoped>
button {
  text-transform: capaitalized;
}
.contrast {
  background-color: green;
  color: #999;
}
</style>
