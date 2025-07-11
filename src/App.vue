<template>
  <div class="wrapper">
    <Header @inputWithDebounce="handleSearchInput"/>
    <Search v-show="searchQuery" :query="searchQuery"/>
    <Catalog/>
  </div>
</template>

<script setup lang="ts">
import Header from "@components/Header/Header.vue";
import Search from "@components/Search/Search.vue";
import {ref, watch} from "vue";
import Catalog from "@components/Catalog/Catalog.vue";

const searchQuery = ref('');
const isLoading = ref(false);

const handleSearchInput = (text: string) => {
  searchQuery.value = text;
};

watch(searchQuery, (newQuery: string) => {
  if (newQuery) {
    console.log('Search query changed:', newQuery);
  }
});
</script>

<style scoped lang="scss">
.wrapper {
  padding: 0 10px;
}
</style>