<template>
  <div class="w-full h-full flex flex-col gap-5 justify-center items-center">
    <h1 class="text-4xl font-bold">Gift Search Bar</h1>
    <input
      type="text"
      class="p-2 border-2 border-gray-dark"
      v-model="searchTerm"
      placeholder="Start typing..."
      @change="searchGift"
    />
    <ul class="list-disc">
      <li v-for="(prod, index) in searchData" :key="index">{{ prod.title }}</li>
    </ul>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const searchTerm = ref('')
const searchData = ref([])

const findProducts = async term => {
  const res = await fetch(`https://dummyjson.com/products/search?q=${term}`)
  const data = await res.json()
  if (term) {
    searchData.value = data.products
  } else {
    searchData.value = []
  }
}

const searchGift = () => {
  findProducts(searchTerm.value)
}
</script>
