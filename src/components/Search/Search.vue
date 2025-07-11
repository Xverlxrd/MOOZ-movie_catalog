<template>
  <div class="search">
    <h1 class="search_title">You searched for:
      <span class="search_query">{{query}}</span>
    </h1>
  </div>
</template>

<script setup lang="ts">
defineProps({
  query: String
})
</script>

<style scoped lang="scss">
.search {
  display: flex;
  gap: 17px;
  align-items: center;
  padding-bottom: 57px;

  &_title {
    font-weight: 400;
    font-size: 22px;
  }

  &_query {
    font-weight: 400;
    font-size: 22px;
    text-decoration: underline;
    text-decoration-style: solid;
  }
}
</style>