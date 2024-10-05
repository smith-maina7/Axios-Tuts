<script setup>
import { ref, onMounted } from 'vue'
import axios from 'axios'

const posts = ref([])
const loading = ref(false)
const error = ref(null)

const fetchPosts = async () => {
  loading.value = true
  error.value = null

  try {
    const res = await axios.get('https://jsonplaceholder.typicode.com/posts')
    posts.value = res.data
  } catch (e) {
    error.value = 'error fetching posts' + e.message
  } finally {
    loading.value = false
  }
}
onMounted(() => fetchPosts())
</script>
<template>
  <div v-for="post in posts" :key="post.id">
    <h2>{{ post.title }}</h2>
    <p>{{ post.body }}</p>
    <hr />
  </div>
</template>
