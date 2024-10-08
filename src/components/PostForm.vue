<script setup>
import axios from 'axios'
import { ref } from 'vue'

const name = ref('')
const email = ref('')
const userName = ref('')
const userResponse = ref(null)

const submitForm = async () => {
  try {
    const response = await axios.post('https://jsonplaceholder.typicode.com/users', {
      name: name.value,
      email: email.value,
      userName: userName.value
    })
    userResponse.value = response.data
    name.value = ''
    email.value = ''
    userName.value = ''
  } catch (error) {
    console.error('Failed to post user data', error)
  }
}
</script>

<template>
  <div class="form-container">
    <h2>Create User</h2>
    <form @submit.prevent="submitForm" class="user-form">
      <div class="form-group">
        <label for="name">Name:</label>
        <input type="text" v-model="name" id="name" />
      </div>

      <div class="form-group">
        <label for="email">Email:</label>
        <input type="email" v-model="email" id="email" />
      </div>

      <div class="form-group">
        <label for="userName">Username:</label>
        <input type="text" v-model="userName" id="userName" />
      </div>

      <button type="submit" class="submit-btn">Submit</button>
    </form>

    <div v-if="userResponse" class="response-message">
      <h3>User Created Successfully:</h3>
      <p><strong>Name:</strong> {{ userResponse.name }}</p>
      <p><strong>Email:</strong> {{ userResponse.email }}</p>
      <p><strong>username:</strong> {{ userResponse.userName }}</p>
    </div>
  </div>
</template>

<style scoped>
.form-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

h2 {
  text-align: center;
  margin-bottom: 20px;
}

.user-form {
  display: flex;
  flex-direction: column;
}

.form-group {
  margin-bottom: 15px;
}

label {
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 8px;
  border: 1px solid #ccc;
  border-radius: 4px;
  box-sizing: border-box;
}

.submit-btn {
  padding: 10px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.submit-btn:hover {
  background-color: #0056b3;
}

.response-message {
  margin-top: 20px;
  padding: 10px;
  background-color: #e8f5e9;
  border: 1px solid #4caf50;
  border-radius: 4px;
  font-style: italic;
  font-size: smaller;
}

.response-message h3 {
  margin-bottom: 10px;
}
</style>
