<template>
  <div>
    <!-- pass pages as ReaderComponent props -->
    <ReaderComponent :pages="pages" />
  </div>
</template>

<script setup lang="ts">
import ReaderComponent from '@/components/ReaderComponent.vue'
import { onMounted, ref } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()
console.log(route.params.id)

const pages = ref<any[]>([])

const getPages = async () => {
  const response = await fetch(
    `https://api.consumet.org/manga/${import.meta.env.VITE_MANGA_SOURCE}/read/${route.params.id}`
  )
  const data = await response.json()
  pages.value = data
  console.log(data)
}

onMounted(() => {
  getPages()
})
</script>
