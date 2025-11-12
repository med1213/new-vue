<template>
  <div>
    <h2>📝 Posts from JSONPlaceholder</h2>

    <div v-if="loading">Loading posts...</div>
    <div v-else-if="error" style="color: red">Error: {{ error }}</div>

    <ul v-else>
      <li v-for="post in posts" :key="post.id">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { getPosts } from "../services/api";

interface Post {
  id: number;
  title: string;
  body: string;
}

const posts = ref<Post[]>([]);
const loading = ref(true);
const error = ref("");

onMounted(async () => {
  try {
    const data = await getPosts();
    posts.value = data;
  } catch (err) {
    error.value = "Failed to fetch posts";
    console.error(err);
  } finally {
    loading.value = false;
  }
});
</script>

<style scoped>
h2 {
  color: #42b883;
}
h3 {
  margin: 8px 0 4px;
  color: #333;
}
p {
  color: #666;
  margin-bottom: 12px;
}
li {
  border-bottom: 1px solid #ddd;
  padding-bottom: 8px;
  margin-bottom: 8px;
}
</style>
