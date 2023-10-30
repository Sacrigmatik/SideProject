<template>
  <div class="search">
    <h1>Search</h1>
    <input type="text" v-model="query" />
    <button @click="search">Search</button>
    <ul>
      <li v-for="manga in mangas" :key="manga?.id">
        <RouterLink :to="{ name: 'MangaDetails', params: { id: manga?.id } }">
          {{ manga?.title }}
        </RouterLink>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
const query = ref<string>('')
const mangas = ref<any>([])

const search = async () => {
  const response = await fetch(
    `https://api.consumet.org/manga/${import.meta.env.VITE_MANGA_SOURCE}/${query.value}`
  )
  const data = await response.json()
  mangas.value = data.results
  console.log(data)
}

//REWRITE THIS BUT OLD VUE 2 STYLE  :
</script>
