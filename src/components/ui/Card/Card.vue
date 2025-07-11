<template>
  <section class="card">
      <img
          class="card_img"
          :src="movie.Poster"
          alt="movie poster"
      />

    <div class="card_content">
      <span class="card_content_text">Name: {{ movie.Title }}</span>
      <span class="card_content_text">Year: {{ movie.Year }}</span>
      <span class="card_content_text">imdbID: {{ movie.imdbID }}</span>
      <span class="card_content_text">Type: {{ movie.Type }}</span>
    </div>
  </section>
</template>

<script setup lang="ts">


import type { Movie } from '@types/movie';

defineProps({
  movie: {
    type: Object as () => Movie,
    required: true,
  }
});

</script>

<style scoped lang="scss">
.card {
  max-width: 245px;
  transition-duration: 0.5s;
  cursor: pointer;

  &_img {
    height: 270px;
    width: 245px;
    object-fit: cover;
    border: 1px solid #3256E3;
    border-radius: 10px;
  }

  &_content {
    display: flex;
    flex-direction: column;
    font-size: 16px;
  }
}
.card:hover {
  transform: scale(110%);
}
</style>