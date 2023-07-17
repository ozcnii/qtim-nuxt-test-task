<template>
  <article class="hentry">
    <header class="entry-header">
      <div class="entry-thumbnail">
        <img
          :alt="post.title"
          :src="imageUrl"
          class="attachment-post-thumbnail size-post-thumbnail wp-post-image"
        />
      </div>
      <h2 style="text-align: center">
        {{ post.title }}
      </h2>
      <span>
        {{ post.description }}
      </span>
    </header>
  </article>
</template>

<script lang="ts" setup>
import { imageUrl } from "~/utils/constants";
import { Post } from "~/utils/types/post";

defineProps<{
  post: Post;
}>();
</script>
