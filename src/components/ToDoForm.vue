<script setup lang="ts">
import { ref } from "vue";

const emit = defineEmits<{
  "add-task": [newTask: string];
}>();

const newTask = ref<string>("");
const error = ref("");

function formSubmitted() {
  if (newTask.value.trim()) {
    emit("add-task", newTask.value.trim());
    newTask.value = "";
  } else {
    error.value = "Task cannot be empty!";
  }
}
</script>

<template>
  <div class="form-container">
    <form @submit.prevent="formSubmitted" class="form">
      <label>
        New Task
        <input
          v-model="newTask"
          name="newTask"
          type="text"
          @input="error = ''"
        />
      </label>

      <button>Add</button>
    </form>
    <p v-if="error">{{ error }}</p>
  </div>
</template>

<style scoped>
.form-container {
  margin: 2rem 0;
}

.form {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 1rem;
}

label {
  font-size: 1.5rem;
}

input {
  background-color: transparent;
  border: 1px solid #999;
  padding: 6px 12px;
  width: 400px;
  color: #bbb;
}

p {
  color: red;
}
</style>
