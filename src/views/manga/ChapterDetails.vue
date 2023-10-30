<template>
  <div class="manga-details">
    <h1>Chapter Details</h1>
    <p>id: {{ $route.params.id }}</p>
  </div>

  <ul>
    <li v-for="page in pages" :key="page?.page">
      <img :src="page?.img" />
    </li>
  </ul>
</template>

<script setup lang="ts">
import { useRoute } from 'vue-router'
import { ref, onMounted } from 'vue'

const route = useRoute()
console.log(route.params.id)

const pages = ref<any>([])

const getPages = async () => {
  const response = await fetch(`https://api.consumet.org/manga/mangadex/read/${route.params.id}`)
  const data = await response.json()
  pages.value = data
  console.log(data)
}

onMounted(() => {
  getPages()
})
</script>

<style scoped>
/* MAKE IMG WIDTH 100% */
img {
  width: 100%;
}
</style>
