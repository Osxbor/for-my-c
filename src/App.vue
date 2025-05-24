<script setup lang="ts">
import { ref } from 'vue';
import BackgroundAnimation from './components/BackgroundAnimation.vue';
import InitialView from './components/InitialView.vue';
import LoveLetter from './components/LoveLetter.vue';
import AudioController from './components/AudioController.vue';

// App state
const showLetter = ref(false);
const audioTrack = ref('intro');

// Function to handle the button click and reveal the letter
const revealLetter = () => {
  showLetter.value = true;
  audioTrack.value = 'letter';
};
</script>

<template>
  <div class="relative overflow-hidden w-full h-full">
    <!-- Background animation -->
    <BackgroundAnimation />

    <!-- Audio controller -->
    <AudioController :track="audioTrack" />

    <!-- Initial view with title and button -->
    <Transition name="fade" mode="out-in" appear>
      <InitialView v-if="!showLetter" @reveal="revealLetter" />
      <LoveLetter v-else />
    </Transition>
  </div>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>