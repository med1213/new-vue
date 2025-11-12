<script setup lang="ts">
import HelloWorld from "./components/HelloWorld.vue";
import PostList from "./components/PostList.vue";
import UserList from "./components/UserList.vue";
import MouseFollower from "./components/MouseFollower.vue";
</script>

<template>
  <HelloWorld msg="What a joke" />

  <div>
    <UserList />
  </div>

  <PostList />

  <MouseFollower>
    <div class="content">
      <h1>Hello Vue Mouse Effect 🐭</h1>
      <p>Move your mouse around!</p>
    </div>
  </MouseFollower>
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}
.logo:hover {
  filter: drop-shadow(0 0 2em #646cffaa);
}
.logo.vue:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
/* .content {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: white;
  font-family: sans-serif;
} */

.content {
  position: absolute;
  top: 40%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: white;
  font-family: "Poppins", sans-serif;
}
</style>
