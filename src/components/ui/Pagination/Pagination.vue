<template>
  <div class="pagination" v-if="totalPages > 1">
    <button
        @click="goToFirstPage"
        :disabled="currentPage === 1"
        class="pagination-button"
    >
      &laquo;
    </button>
    <button
        @click="goToPrevPage"
        :disabled="currentPage === 1"
        class="pagination-button"
    >
      &lsaquo;
    </button>

    <template v-for="page in visiblePages" :key="page">
      <button
          v-if="page === '...'"
          class="pagination-ellipsis"
          disabled
      >
        ...
      </button>
      <button
          v-else
          @click="goToPage(page)"
          :class="['pagination-button', { 'active': page === currentPage }]"
      >
        {{ page }}
      </button>
    </template>

    <button
        @click="goToNextPage"
        :disabled="currentPage >= totalPages"
        class="pagination-button"
    >
      &rsaquo;
    </button>
    <button
        @click="goToLastPage"
        :disabled="currentPage >= totalPages"
        class="pagination-button"
    >
      &raquo;
    </button>
  </div>
</template>

<script setup lang="ts">
import { computed } from 'vue';

const props = defineProps({
  currentPage: {
    type: Number,
    required: true,
    validator: (value: number) => value > 0
  },
  totalPages: {
    type: Number,
    required: true,
    validator: (value: number) => value > 0
  },
  maxVisible: {
    type: Number,
    default: 5
  }
});

const emit = defineEmits(['pageChanged']);

const visiblePages = computed(() => {
  const pages = [];
  let startPage = Math.max(1, props.currentPage - Math.floor(props.maxVisible / 2));
  let endPage = Math.min(props.totalPages, startPage + props.maxVisible - 1);

  if (endPage - startPage + 1 < props.maxVisible) {
    startPage = Math.max(1, endPage - props.maxVisible + 1);
  }

  if (startPage > 1) {
    pages.push(1);
    if (startPage > 2) {
      pages.push('...');
    }
  }

  for (let i = startPage; i <= endPage; i++) {
    if (i >= 1 && i <= props.totalPages) {
      pages.push(i);
    }
  }

  if (endPage < props.totalPages) {
    if (endPage < props.totalPages - 1) {
      pages.push('...');
    }
    pages.push(props.totalPages);
  }

  return pages;
});

const goToPage = (page: number) => {
  if (page >= 1 && page <= props.totalPages && page !== props.currentPage) {
    emit('pageChanged', page);
  }
};

const goToFirstPage = () => goToPage(1);
const goToLastPage = () => goToPage(props.totalPages);
const goToPrevPage = () => goToPage(props.currentPage - 1);
const goToNextPage = () => goToPage(props.currentPage + 1);
</script>

<style scoped lang="scss">
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 8px;
  margin: 30px 0;
  flex-wrap: wrap;
}

.pagination-button {
  padding: 8px 12px;
  min-width: 36px;
  background-color: #f5f5f5;
  color: #333;
  border: 1px solid #ddd;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s;

  &:hover:not(:disabled) {
    background-color: #e9e9e9;
  }

  &:disabled {
    opacity: 0.5;
    cursor: not-allowed;
  }

  &.active {
    background-color: #3256E3;
    color: white;
    border-color: #3256E3;
  }
}

.pagination-ellipsis {
  padding: 8px 12px;
  border: none;
  background: transparent;
  cursor: default;
}
</style>