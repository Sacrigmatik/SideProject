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
  </div>
</template>

<script setup lang="ts">
import { useRoute } from 'vue-router'
import { ref, onMounted } from 'vue'

// https://api.consumet.org/manga/mangadex/info/{route.params.id}

const route = useRoute()
console.log(route.params.id)

const chapters = ref<any>([])

const getChapters = async () => {
  const response = await fetch(`https://api.consumet.org/manga/mangadex/info/${route.params.id}`)
  const data = await response.json()
  chapters.value = data?.chapters
  console.log('CHAPTERS :')
  console.log(data?.chapters)
}

onMounted(() => {
  getChapters()
})
</script>
