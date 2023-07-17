<template>
  <article class="hentry">
    <header class="entry-header">
      <div class="entry-thumbnail">
        <NuxtLink :to="`/posts/${post.id}`"
          ><img
            :alt="post.title"
            :src="imageUrl"
            class="attachment-post-thumbnail size-post-thumbnail wp-post-image"
        /></NuxtLink>
      </div>
      <h2 class="entry-title">
        <NuxtLink :to="`/posts/${post.id}`" rel="bookmark"
          >{{ post.title }} {{ post.id }}
        </NuxtLink>
      </h2>
      <span>
        {{ post.preview }}
      </span>
    </header>
  </article>
</template>

<script lang="ts" setup>
import { Post } from "~/utils/types/post";
// TODO: ваша api дает нерабочую ссылку на картинку
import { imageUrl } from "~/utils/constants";

defineProps<{
  post: Post;
}>();
</script>
