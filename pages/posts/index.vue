<template>
  <div id="content" class="site-content">
    <div id="primary" class="content-area column full">
      <PostsPageContent v-if="data" :allPosts="data" />

      <div v-if="pending">Loading...</div>

      <div v-if="error" style="color: red">ERROR: {{ error.data }}</div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { Post } from "~/utils/types/post";
import { BASE_API_URL } from "~/utils/constants";

const url = BASE_API_URL + "posts";

const { data, pending, error } = await useFetch<Post[]>(url, {
  server: true,
  lazy: false,
});
</script>
