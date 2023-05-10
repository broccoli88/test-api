<script setup lang="ts">
import useFetch from '@/dist/useFetch'
import { useRoute } from 'vue-router'
import { reactive, onMounted, watch } from 'vue'

const route = useRoute()
const joke = reactive<any>({ list: [] })

onMounted(async () => {
  const url = `https://v2.jokeapi.dev/joke/${route.params.category}`
  const { response, fetchData } = useFetch(url, {})

  await fetchData()
  joke.list = response.value
  console.log(joke.list)
})

watch(
  () => route.params.category,
  async () => {
    const url = `https://v2.jokeapi.dev/joke/${route.params.category}`
    const { response, fetchData } = useFetch(url, {})

    await fetchData()
    joke.list = response.value
    console.log(joke.list)
  }
)
</script>

<template>
  <div>
    <h1>{{ route.params.category }}</h1>
    <div v-if="joke.list">
      <p>{{ joke.list.setup }}</p>
      <p>{{ joke.list.delivery }}</p>
    </div>
    <p v-else>Loading...</p>
  </div>
</template>

<style scoped>
h1 {
  margin-bottom: 4rem;
}
</style>
