<script setup lang="ts">
import useFetch from '@/dist/useFetch'
import { reactive, onMounted } from 'vue'

const url = ' https://v2.jokeapi.dev/categories'
const { response, fetchData } = useFetch(url, {})
const jokeCategoriesList = reactive<any>({ list: [] })

onMounted(async () => {
  await fetchData()
  jokeCategoriesList.list = response.value
  console.log(jokeCategoriesList.list)
})
</script>
<template>
  <div>
    <nav>
      <ul>
        <li v-for="category in jokeCategoriesList.list.categories" :key="category">
          <router-link :to="`/category/${category}`">{{ category }}</router-link>
        </li>
      </ul>
    </nav>
  </div>
</template>

<style scoped>
nav {
  margin-bottom: 4rem;
}

ul {
  display: flex;
  gap: 3rem;
  list-style: none;
}
</style>
