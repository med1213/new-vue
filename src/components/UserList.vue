<template>
  <div>
    <h2>👥 User List (from JSONPlaceholder)</h2>

    <ul v-if="users.length > 0">
      <li v-for="user in users" :key="user.id">
        <strong>{{ user.name }}</strong> — {{ user.email }}
      </li>
    </ul>

    <p v-else>Loading users...</p>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { getUsers } from "../services/api";

interface User {
  id: number;
  name: string;
  email: string;
}

const users = ref<User[]>([]);

onMounted(async () => {
  try {
    const data = await getUsers();
    users.value = data;
  } catch (error) {
    console.error("Error fetching users:", error);
  }
});
</script>

<style scoped>
h2 {
  color: #42b883;
}
li {
  margin-bottom: 6px;
}
</style>
