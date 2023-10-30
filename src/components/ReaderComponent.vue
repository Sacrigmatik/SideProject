<template>
  <div class="container">
    <button v-if="currentPageNumber > 0" @click="currentPageNumber--" class="left-arrow">
      &lt;
    </button>
    <img :src="pages[currentPageNumber]?.img" />
    <button
      v-if="currentPageNumber < pages.length - 1"
      @click="currentPageNumber++"
      class="right-arrow"
    >
      &gt;
    </button>
  </div>
</template>

<script setup lang="ts">
import { ref, type PropType } from 'vue'

interface Chapter {
  img: string
  page: number
}

defineProps({
  pages: {
    type: Array as PropType<Chapter[]>,
    required: true
  }
})

const currentPageNumber = ref<number>(0)
</script>

<style scoped>
/* BOOK READER STYLE, ARROWS ALWAYS AT THE SAME PLACE AND THE ARROWS MUST NOT OVERLAP THE IMAGE*/
.container {
  position: relative;
  width: 100%;
  height: 100%;
}

.container img {
  width: 100%;
  height: 100%;
  object-fit: contain;
}

.left-arrow {
  width: 70px;
  height: 70px;
  position: absolute;
  top: 50%;
  left: 0;
  transform: translateY(-50%);
  background-color: #00000028;
  border-radius: 100px;
  border: none;
  font-size: 2rem;
  color: white;
  cursor: pointer;
}

.right-arrow {
  width: 70px;
  height: 70px;
  position: absolute;
  top: 50%;
  right: 0;
  transform: translateY(-50%);
  background-color: #00000028;
  border-radius: 100px;
  border: none;
  font-size: 2rem;
  color: white;
  cursor: pointer;
}
</style>
