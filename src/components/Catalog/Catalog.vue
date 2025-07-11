<template>
  <main class="catalog">
    <Card
        v-for="movie in movies"
        :key="movie.imdbID"
        :movie="movie"
    />
  </main>
</template>

<script setup lang="ts">
import {onMounted, ref} from "vue";
import Card from "@components/ui/Card/Card.vue";
import type {Movie} from "@types";

const movies = ref<Movie[]>([]);

const fetchApi = async () => {
  const response = await fetch('https://www.omdbapi.com/?i=tt3896198&apikey=8523cbb8&s=Batman&page=2');
  const data = await response.json();
  movies.value = data.Search;
}

onMounted(() => {
  fetchApi();
})

</script>

<style scoped>
.catalog {
  display: flex;
  flex-wrap: wrap;
  gap: 45px;
  padding-bottom: 84px;
}
</style>