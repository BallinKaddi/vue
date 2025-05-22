<template>
  <div class="container">
    <h2>Search Discord Links</h2>
    <input
      v-model="searchQuery"
      type="text"
      placeholder="Search..."
      class="search-input"
    />
    <ul v-if="filteredItems.length" class="results-list">
      <li v-for="(item, index) in filteredItems" :key="index" class="result-item">
        <img :src="item.image" alt="" class="item-image" />
        <div class="item-info">
          <strong class="item-title">{{ item.title }}</strong>
          <a
            :href="item.description"
            target="_blank"
            rel="noopener noreferrer"
            class="link-button"
          >
            Visit Link
          </a>
        </div>
      </li>
    </ul>
    <p v-else>No results found.</p>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import jsonDataRaw from '../data/data.json'

const jsonData = ref(jsonDataRaw)
const searchQuery = ref('')

const filteredItems = computed(() => {
  const q = searchQuery.value.toLowerCase()
  return jsonData.value.filter(
    item =>
      item.title.toLowerCase().includes(q) ||
      item.description.toLowerCase().includes(q)
  )
})
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 40px auto;
  padding: 0 16px;
  font-family: Arial, sans-serif;
  color: #222;
  text-align: center;
}

h2 {
  margin-bottom: 20px;
}

.search-input {
  width: 100%;
  padding: 10px 14px;
  font-size: 16px;
  border: 1.5px solid #ccc;
  border-radius: 6px;
  box-sizing: border-box;
  margin-bottom: 24px;
  transition: border-color 0.2s ease;
}

.search-input:focus {
  outline: none;
  border-color: #555;
}

.results-list {
  list-style: none;
  padding: 0;
  margin: 0;
  text-align: left;
}

.result-item {
  display: flex;
  align-items: center;
  padding: 12px 0;
  border-bottom: 1px solid #eee;
  gap: 16px;
}

.item-image {
  width: 60px;
  height: 60px;
  object-fit: cover;
  border-radius: 8px;
  flex-shrink: 0;
}

.item-info {
  flex-grow: 1;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 12px;
}

.item-title {
  font-size: 1.1em;
  word-break: break-word;
}

.link-button {
  padding: 6px 12px;
  background-color: #007bff;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  font-size: 0.9em;
  white-space: nowrap;
  transition: background-color 0.2s ease;
}

.link-button:hover {
  background-color: #0056b3;
}

p {
  color: #555;
  font-style: italic;
  margin-top: 20px;
}

/* Responsive on smaller phones */
@media (max-width: 480px) {
  .result-item {
    flex-direction: column;
    align-items: flex-start;
    gap: 12px;
  }
  .item-info {
    flex-direction: column;
    align-items: flex-start;
    gap: 8px;
  }
  .link-button {
    width: 100%;
    text-align: center;
  }
  .item-image {
    width: 100%;
    height: auto;
    border-radius: 6px;
  }
}
</style>
