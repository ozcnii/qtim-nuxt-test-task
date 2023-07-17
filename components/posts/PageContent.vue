<template>
  <main id="main" class="site-main">
    <div class="grid portfoliogrid" style="display: flex; flex-wrap: wrap">
      <PostsShortItem v-for="post in posts" :post="post" :key="post.id" />
    </div>

    <SharedPagination
      :currentPage="currentPage"
      :lastPage="lastPage"
      @nextPage="() => (currentPage += 1)"
      @prevPage="() => (currentPage -= 1)"
      @setCurrentPage="(v: number) => (currentPage = v)"
    />
  </main>
</template>

<script lang="ts" setup>
import { POSTS_PER_PAGE } from "~/utils/constants";
import { Post } from "~/utils/types/post";

const props = defineProps<{
  allPosts: Post[];
}>();

const route = useRoute();
const router = useRouter();

const posts = ref<Post[]>();
const currentPage = ref(1);
const lastPage = Math.ceil(props.allPosts.length / POSTS_PER_PAGE);

onMounted(() => {
  const page = route.query.page;
  if (page) {
    currentPage.value = Number(page);
  }
});

watch(currentPage, () => {
  router.push({
    path: route.path,
    query: { ...route.query, page: currentPage.value },
  });
});

watchEffect(() => {
  posts.value = props.allPosts.slice(
    (currentPage.value - 1) * POSTS_PER_PAGE,
    currentPage.value * POSTS_PER_PAGE,
  );
});
</script>
