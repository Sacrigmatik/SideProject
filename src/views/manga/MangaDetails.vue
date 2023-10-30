<template>
  <div class="manga-details">
    <h1>Manga Details</h1>
    <p>id: {{ $route.params.id }}</p>
    <ul>
      <li v-for="chapter in chapters" :key="chapter?.id">
        <RouterLink :to="{ name: 'ChapterDetails', params: { id: chapter?.id } }">
          {{ chapter?.title }}
        </RouterLink>
      </li>
    </ul>
    <div v-if="chapters.length === 0">Loading...</div>
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
console.log(route.params.id)

const chapters = ref<any>([])

const getChapters = async () => {
  const response = await fetch(
    `https://api.consumet.org/manga/${import.meta.env.VITE_MANGA_SOURCE}/info/${route.params.id}`
  )
  const data = await response.json()
  chapters.value = data?.chapters
  console.log('CHAPTERS :')
  console.log(data?.chapters.reverse())
}

onMounted(() => {
  getChapters()
})
</script>
