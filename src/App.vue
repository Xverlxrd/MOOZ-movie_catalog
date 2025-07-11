<template>
  <div class="wrapper">
    <Header @inputWithDebounce="handleSearchInput"/>
    <Search v-show="searchQuery" :query="searchQuery"/>
    <Catalog
        v-if="movies.length"
        :movies="movies"
        :loading="isLoading"/>
    <h1 v-else>
      Not found
    </h1>
    <Pagination
        v-if="totalPages > 1"
        :current-page="currentPage"
        :total-pages="totalPages"
        @pageChanged="handlePageChange"
    />
  </div>
</template>

<script setup lang="ts">
import Header from "@components/Header/Header.vue";
import Search from "@components/Search/Search.vue";
import Catalog from "@components/Catalog/Catalog.vue";
import { ref, computed, watch } from "vue";
import type { Movie } from "@/types.d.ts";
import Pagination from "@components/ui/Pagination/Pagination.vue";

const searchQuery = ref('');
const isLoading = ref(false);
const movies = ref<Movie[]>([]);
const currentPage = ref(1);
const totalResults = ref(0);
const apiKey = '8523cbb8'; // Вынесите в .env файл

const totalPages = computed(() => Math.ceil(totalResults.value / 10));

const handlePageChange = (newPage: number) => {
  currentPage.value = newPage;
};

const handleSearchInput = (text: string) => {
  searchQuery.value = text;
  currentPage.value = 1;
};

const fetchMovies = async () => {
  try {
    isLoading.value = true;
    const response = await fetch(
        `https://www.omdbapi.com/?apikey=${apiKey}&s=${searchQuery.value || 'Batman'}&page=${currentPage.value}`
    );
    const data = await response.json();

    if (data.Response === 'True') {
      movies.value = data.Search;
      totalResults.value = parseInt(data.totalResults);
    } else {
      movies.value = [];
      totalResults.value = 0;
      console.error(data.Error || 'Unknown error');
    }
  } catch (error) {
    console.error('Failed to fetch movies:', error);
    movies.value = [];
  } finally {
    isLoading.value = false;
  }
};

watch([currentPage, searchQuery], fetchMovies, { immediate: true });
</script>

<style scoped lang="scss">
.wrapper {
  padding: 0 10px;
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>