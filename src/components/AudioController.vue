<script setup lang="ts">
import { ref, watch, onMounted } from 'vue';

const props = defineProps<{
  track: string;
}>();

const audioElement = ref<HTMLAudioElement | null>(null);
const audioSources = {
  intro: '/music-intro.mp3',
  letter: '/music-letter.mp3'
};

// Watch for track changes and update the audio source
watch(() => props.track, (newTrack) => {
  if (audioElement.value && audioSources[newTrack as keyof typeof audioSources]) {
    audioElement.value.src = audioSources[newTrack as keyof typeof audioSources];
    audioElement.value.play().catch(error => {
      console.warn('Audio autoplay was prevented:', error);
    });
  }
});

// Initialize audio when component mounts
onMounted(() => {
  if (audioElement.value) {
    // Set initial source
    audioElement.value.src = audioSources[props.track as keyof typeof audioSources];
    audioElement.value.loop = true;
    
    // Try to play audio (might be blocked by browser autoplay policies)
    audioElement.value.play().catch(error => {
      console.warn('Audio autoplay was prevented:', error);
    });
  }
});

// Toggle audio playback
const toggleAudio = () => {
  if (!audioElement.value) return;
  
  if (audioElement.value.paused) {
    audioElement.value.play();
  } else {
    audioElement.value.pause();
  }
};
</script>

<template>
  <div class="audio-controller fixed top-4 right-4 z-50">
    <audio ref="audioElement" loop></audio>
    
    <button 
      @click="toggleAudio"
      class="bg-secondary bg-opacity-20 hover:bg-opacity-30 p-3 rounded-full transition-all duration-300"
      title="Toggle music"
    >
      <!-- Simple audio icon -->
      <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-secondary">
        <path d="M9 18V5l12-2v13"></path>
        <circle cx="6" cy="18" r="3"></circle>
        <circle cx="18" cy="16" r="3"></circle>
      </svg>
    </button>
  </div>
</template>

<style scoped>
/* Subtle hover effect for the audio button */
button:hover {
  transform: scale(1.05);
}
</style>