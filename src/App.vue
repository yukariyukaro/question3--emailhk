<template>
  <div :class="{'dark-mode': isDarkMode}">
    <div class="container">
      <input
        v-model="email"
        @input="validateEmail"
        :class="{'invalid': !isValid, 'valid': isValid}"
        type="text"
        placeholder="Enter your HKU email"
      />
      <button :disabled="!isValid" :class="{'disabled': !isValid}" @click="handleSubmit">
        Submit
      </button>
      <p v-if="uid">UID: {{ uid }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';

// Define reactive variables
const email = ref('');
const uid = ref('');
const isDarkMode = ref(window.matchMedia('(prefers-color-scheme: dark)').matches);

// Computed property to check email validity
const isValid = computed(() => {
  const regex = /^[^\s@]+@(connect\.hku\.hk|hku\.hk)$/;
  return regex.test(email.value);
});

// Method to handle email validation
function validateEmail() {
  // Computed property will automatically update
}

// Method to handle form submission
function handleSubmit() {
  if (isValid.value) {
    const [userId] = email.value.split('@');
    uid.value = userId;
  }
}
</script>

<style>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
}

input {
  padding: 10px;
  margin-bottom: 10px;
  border: 2px solid #ccc;
  border-radius: 4px;
}

input.valid {
  border-color: green;
}

input.invalid {
  border-color: red;
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

button.disabled {
  background-color: gray;
  cursor: not-allowed;
}

.dark-mode {
  background-color: #121212;
  color: white;
}

.dark-mode input,
.dark-mode button {
  background-color: #1e1e1e;
  color: white;
  border: 2px solid #555;
}

.dark-mode input.valid {
  border-color: lightgreen;
}

.dark-mode input.invalid {
  border-color: lightcoral;
}
</style>

