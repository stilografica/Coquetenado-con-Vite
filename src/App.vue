<script setup>
import { ref, onMounted } from 'vue'

import BlogPost from '@/components/BlogPost.vue'

// Constants
const title = "Mi blog"
const posts = ref([])
const init = ref(0)
const final = ref(10)
const loading = ref(false)

// Functions
const handlePagination = (type) => {
  loading.value = true
  // So that it seems that we make calls to the api
  setTimeout(() => {
    if (type === 'prev') {
      init.value -= 11
      final.value -= 11
    } else {
      init.value += 11
      final.value += 11
    }
    loading.value = false
  }, 1000);
}
onMounted(async () => {
  loading.value = true
  // Fetch data
  try {
    await fetch("https://jsonplaceholder.typicode.com/posts")
    .then((res) => res.json())
    .then((data) => (posts.value = data))
    .finally(() => (loading.value = false))
  } catch(e) {
      console.log(e)
  }
})
</script>

<template>
  <div class="container mt-4">
    <h1 class="text-center">{{title}}</h1>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button :disabled="init <= 0" type="button" class="btn btn-outline-primary" @click="handlePagination('prev')">Anterior</button>
        <button :disabled="final > posts.length-1" type="button" class="btn btn-outline-primary" @click="handlePagination('next')">Siguiente</button>
    </div>
    <div v-if="loading" class="d-flex justify-content-center">
      <div class="spinner-border text-primary" role="status">
      </div>
    </div>
  <div v-else>
    <blog-post
      v-for="post in posts.slice(init, final)"
      :key="post.id"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      class="text-capitalize"
    />
  </div>
</div>
</template>

<style scoped>
</style>
