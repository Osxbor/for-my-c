<script setup lang="ts">
import { onMounted } from 'vue';
import { gsap } from 'gsap';

const props = defineProps<{}>();
const emit = defineEmits(['reveal']);

// Animate only the title when mounted
onMounted(() => {
  // Title animation
  gsap.from('.title', {
    y: 50,
    opacity: 0,
    duration: 1.5,
    ease: 'back.out(1.7)'
  });

  // Simple fade in for button
  gsap.from('.reveal-button', {
    opacity: 0,
    duration: 1,
    delay: 0.5
  });
});

// Handle the button click
const handleReveal = () => {
  // Button click animation
  gsap.to('.reveal-button', {
    scale: 0.95,
    duration: 0.1,
    yoyo: true,
    repeat: 1,
    onComplete: () => emit('reveal')
  });
};
</script>

<template>
  <div class="flex flex-col items-center justify-center h-screen px-4">
    <h1 class="title text-4xl md:text-5xl lg:text-6xl font-bold text-secondary mb-8 text-center">
      Un pequeño detalle para alguien muy especial.
    </h1>

    <button @click="handleReveal"
      class="px-8 py-4 text-xl bg-accent-purple hover:bg-opacity-90 text-white rounded-full shadow-lg transition-all duration-300 hover:shadow-xl transform hover:-translate-y-1">
      ¿Que será esto?
    </button>
  </div>
</template>

<style scoped>
/* Button hover effects */
.reveal-button:hover {
  box-shadow: 0 0 15px rgba(197, 131, 235, 0.5);
}
</style>