<template>
  <div class="bubble-area">
    <div
      class="bubble"
      :style="{
        transform: `translate(${x}px, ${y}px) scale(${scale})`,
        background: color,
      }"
    ></div>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted, onUnmounted } from "vue";

// Reactive mouse and animation data
const x = ref(window.innerWidth / 2);
const y = ref(window.innerHeight / 2);
const targetX = ref(x.value);
const targetY = ref(y.value);
const scale = ref(1);
const color = ref("rgba(66, 184, 131, 0.5)");

// Handle mouse movement
function handleMouseMove(e: MouseEvent) {
  targetX.value = e.clientX;
  targetY.value = e.clientY;
  scale.value = 1.2;
  color.value = "rgba(100, 255, 218, 0.8)";
}

// Smooth animation using easing
function animate() {
  x.value += (targetX.value - x.value) * 0.1;
  y.value += (targetY.value - y.value) * 0.1;

  // Smoothly shrink back
  scale.value += (1 - scale.value) * 0.1;
  color.value = `rgba(100, 255, 218, ${0.4 + (scale.value - 1) * 2})`;

  requestAnimationFrame(animate);
}

onMounted(() => {
  window.addEventListener("mousemove", handleMouseMove);
  animate();
});

onUnmounted(() => {
  window.removeEventListener("mousemove", handleMouseMove);
});
</script>

<style scoped>
.bubble-area {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  pointer-events: none;
  background: #0f0f0f;
}

.bubble {
  position: absolute;
  width: 60px;
  height: 60px;
  border-radius: 50%;
  backdrop-filter: blur(8px);
  box-shadow: 0 0 40px rgba(100, 255, 218, 0.6);
  pointer-events: none;
  mix-blend-mode: screen;
  transition: transform 0.2s ease-out;
}
</style>
