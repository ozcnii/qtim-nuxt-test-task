<template>
  <div class="pagination">
    <button v-show="currentPage !== 1" @click="emit('prevPage')">Prev</button>

    <button
      v-show="currentPage > 2"
      @click="emit('setCurrentPage', currentPage - 2)"
    >
      {{ currentPage - 2 }}
    </button>

    <button
      v-show="currentPage > 1"
      @click="emit('setCurrentPage', currentPage - 1)"
    >
      {{ currentPage - 1 }}
    </button>

    <span class="current">{{ currentPage }}</span>

    <button
      v-show="lastPage - currentPage > 0"
      @click="emit('setCurrentPage', currentPage + 1)"
    >
      {{ currentPage + 1 }}
    </button>

    <button
      v-show="lastPage - currentPage > 1"
      @click="emit('setCurrentPage', currentPage + 2)"
    >
      {{ currentPage + 2 }}
    </button>

    <template v-if="currentPage !== lastPage && currentPage + 2 < lastPage">
      <span>...</span>
      <button @click="emit('setCurrentPage', lastPage)">{{ lastPage }}</button>
    </template>

    <button v-show="currentPage !== lastPage" @click="emit('nextPage')">
      Next
    </button>
  </div>
</template>

<script lang="ts" setup>
defineProps<{
  currentPage: number;
  lastPage: number;
}>();

const emit = defineEmits<{
  (e: "prevPage"): void;
  (e: "nextPage"): void;
  (e: "setCurrentPage", id: number): void;
}>();
</script>
