<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { gsap } from 'gsap';

const particles = ref<Array<{ x: number, y: number, size: number, speed: number }>>([]);
const canvas = ref<HTMLCanvasElement | null>(null);
const ctx = ref<CanvasRenderingContext2D | null>(null);

// Create particles for the animation
const createParticles = () => {
  for (let i = 0; i < 50; i++) {
    particles.value.push({
      x: Math.random() * window.innerWidth,
      y: Math.random() * window.innerHeight,
      size: Math.random() * 3 + 1,
      speed: Math.random() * 1 + 0.2
    });
  }
};

// Animate the particles
const animateParticles = () => {
  if (!canvas.value || !ctx.value) return;

  ctx.value.clearRect(0, 0, canvas.value.width, canvas.value.height);
  ctx.value.fillStyle = '#E2E7ED';
  
  particles.value.forEach(particle => {
    ctx.value!.globalAlpha = 0.6; // Semi-transparent particles
    ctx.value!.beginPath();
    ctx.value!.arc(particle.x, particle.y, particle.size, 0, Math.PI * 2);
    ctx.value!.fill();
    
    // Move particles upward
    particle.y -= particle.speed;
    
    // Reset position if particle goes off screen
    if (particle.y < 0) {
      particle.y = window.innerHeight;
      particle.x = Math.random() * window.innerWidth;
    }
  });
  
  requestAnimationFrame(animateParticles);
};

// Initialize the canvas and animation
onMounted(() => {
  if (canvas.value) {
    ctx.value = canvas.value.getContext('2d');
    canvas.value.width = window.innerWidth;
    canvas.value.height = window.innerHeight;
    
    createParticles();
    animateParticles();
    
    // Add some GSAP animations for the background
    gsap.to('.background-overlay', {
      opacity: 0.3,
      duration: 4,
      repeat: -1,
      yoyo: true,
      ease: 'sine.inOut'
    });
  }
  
  // Handle window resize
  window.addEventListener('resize', () => {
    if (canvas.value) {
      canvas.value.width = window.innerWidth;
      canvas.value.height = window.innerHeight;
    }
  });
});
</script>

<template>
  <div class="fixed top-0 left-0 w-full h-full -z-10">
    <div class="background-overlay absolute top-0 left-0 w-full h-full bg-gradient-to-tr from-primary to-accent-purple opacity-10"></div>
    <canvas ref="canvas" class="absolute top-0 left-0 w-full h-full"></canvas>
  </div>
</template>

<style scoped>
/* No additional styles needed as everything is handled by Tailwind and inline styles */
</style>