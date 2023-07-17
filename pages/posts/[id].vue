<template>
  <div style="text-align: center">
    <PostsItem v-if="data" :post="data" />

    <div v-if="pending">Loading...</div>

    <div v-if="error" style="color: red">ERROR: {{ error.data }}</div>
  </div>
</template>

<script lang="ts" setup>
import { Post } from "~/utils/types/post";
import { BASE_API_URL } from "~/utils/constants";

const route = useRoute();
const url = BASE_API_URL + "posts/" + route.params.id;

const { data, pending, error } = useFetch<Post>(url, {
  server: true,
  lazy: false,
});
</script>
