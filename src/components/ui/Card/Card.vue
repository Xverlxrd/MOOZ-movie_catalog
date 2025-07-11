<template>
  <section class="card">
    <div class="card_img-container">
      <img
          class="card_img"
          :src="posterUrl"
          :alt="`${movie.Title} poster`"
          @error="handleImageError"
      />
      <div v-if="showPlaceholder" class="card_placeholder">
        <img :src="NoImg" alt="No poster available" class="placeholder-image"/>
      </div>
    </div>

    <div class="card_content">
      <span class="card_content_text">Name: {{ movie.Title }}</span>
      <span class="card_content_text">Year: {{ movie.Year }}</span>
      <span class="card_content_text">imdbID: {{ movie.imdbID }}</span>
      <span class="card_content_text">Type: {{ movie.Type }}</span>
    </div>
  </section>
</template>

<script setup lang="ts">
import NoImg from '@assets/noImg.png'
import type {Movie} from "@/types/movie.d.ts";
import {computed, ref} from "vue";

const props = defineProps({
  movie: {
    type: Object as () => Movie,
    required: true,
  }
});

const imageError = ref(false);

const posterUrl = computed(() => {
  return props.movie.Poster && props.movie.Poster !== 'N/A'
      ? props.movie.Poster
      : '';
});

const showPlaceholder = computed(() => {
  return !props.movie.Poster || props.movie.Poster === 'N/A' || imageError.value;
});

const handleImageError = () => {
  imageError.value = true;
};

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