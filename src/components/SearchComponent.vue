<template>
  <div>
    <input v-model="search" placeholder="Search..." />

    <div v-for="item in filteredItems" :key="item.title" style="margin-bottom: 1rem;">
      <h3>{{ item.title }}</h3>
      <a :href="item.description" target="_blank" rel="noopener noreferrer">{{ item.description }}</a>
      <img :src="item.image" alt="image" style="width: 100px; height: auto; margin-top: 0.5rem;" />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const items = ref([])
const search = ref('')

onMounted(async () => {
  try {
    const res = await fetch('/data.json')
    items.value = await res.json()
  } catch (error) {
    console.error('Failed to load JSON:', error)
  }
})

const filteredItems = computed(() => {
  if (!search.value) return items.value
  return items.value.filter(item =>
    item.title.toLowerCase().includes(search.value.toLowerCase())
  )
})
</script>

<style scoped>
input {
  padding: 0.5rem;
  font-size: 1rem;
  margin-bottom: 1rem;
  width: 100%;
  max-width: 400px;
  box-sizing: border-box;
}
</style>
