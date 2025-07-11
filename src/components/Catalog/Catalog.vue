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
import Card from "@components/ui/Card/Card.vue";
import type {Movie} from "@/types/movie.d.ts";
import type {PropType} from "vue";

defineProps({
  movies: {
    type: Array as PropType<Movie[]>,
    required: true
  }
})
</script>

<style scoped>
.catalog {
  display: flex;
  flex-wrap: wrap;
  gap: 45px;
  padding-bottom: 84px;
}
@media (max-width: 1424px) {
  .catalog {
    justify-content: center;
  }
}
</style>