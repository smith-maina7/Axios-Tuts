<script setup>
import { ref } from 'vue'
import axios from 'axios'

// const title = ref('')
// const body = ref('')
// const response = ref(null)
const userFirstName = ref([])
const userLastName = ref([])
const email = ref('')
const user = ref('')

// const submitPost = async () => {
//   try {
//     const res = await axios.post('https://jsonplaceholder.typicode.com/posts', {
//       title: title.value,
//       body: body.value,
//       userId: 1
//     })
//     response.value = res.data
//     title.value = ''
//     body.value = ''
//   } catch (error) {
//     console.error('There was an error!', error)
//   }
// }

const submitUser = async () => {
  try {
    const res = await axios.post('https://jsonplaceholder.typicode.com/posts', {
      firstName: userFirstName.value,
      lastName: userLastName.value,
      email: email.value
    })
    user.value = res.data
    const fullName = `${user.value.firstName} ${user.value.lastName}`
    userFirstName.value = ''
    userLastName.value = ''
    email.value = ''
    return fullName
  } catch (error) {
    console.error('There was an error!', error)
  }
}
</script>

<template>
  <!-- <div>
    <form @submit.prevent="submitPost">
      <input v-model="title" placeholder="Title" required />
      <textarea v-model="body" placeholder="Body" required></textarea>
      <button type="submit">Submit Post</button>
    </form>
    <p v-if="response">Response: {{ response }}</p>
  </div> -->
  <div>
    <form @submit.prevent="submitUser">
      <input type="text" placeholder="First name" v-model="firstName" />
      <input type="text" placeholder="last name" v-model="lastName" />
      <input type="email" placeholder="email address" v-model="email" />
      <button type="submit">Submit Post</button>
    </form>
  </div>
  <p v-if="fullName">User Name: {{ fullName }}</p>
</template>

<style scoped>
.form-container {
  max-width: 400px;
  margin: 0 auto;
  padding: 20px;
  border: 1px solid #ccc;
  border-radius: 8px;
  background-color: #f9f9f9;
}

form {
  display: flex;
  flex-direction: column;
}

input,
textarea {
  margin-bottom: 10px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 10px;
  border: none;
  border-radius: 4px;
  background-color: #007bff;
  color: white;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}
</style>
