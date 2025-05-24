<script setup lang="ts">
import { onMounted, ref } from 'vue';
import { gsap } from 'gsap';

// The content of the love letter - Replace this with your actual message
const letterContent = ref(`
Para Ti, Mi Amor

Desde el momento en que llegaste a mi vida,
todo cambió de color, todo cobró sentido.
Tus ojos son el refugio donde encuentro paz,
tus risas son la brisa que calma mi corazón.

Cada palabra tuya es música para mi alma,
cada gesto tuyo despierta mariposas en mi pecho.
Contigo he descubierto finalmente lo que significa amar,
contigo he encontrado el hogar que tanto busqué.

Eres la razón por la que cada mañana
despierto con ganas de ser mejor persona.
Eres mi cómplice, mi confidente, mi sueño hecho realidad,
eres todo lo que no sabía que necesitaba.

Contigo el tiempo se detiene,
en tus ojos encuentro mi futuro.

Quiero estar a tu lado cada día,
construir juntos nuestra propia historia.
Eres especial, única, extraordinaria,
eres la dueña de mi corazón.

Y aunque las palabras se queden cortas
para expresar todo lo que siento,
quiero que sepas que te amo
con cada fibra de mi ser.

Con todo mi amor,
Un chico muy enamorado de ti <3
`);

// Animate the letter when it appears
onMounted(() => {
  // Paper animation
  gsap.from('.letter-container', {
    scale: 0.7,
    opacity: 0,
    duration: 1.2,
    ease: 'elastic.out(1, 0.75)'
  });

  // Text animation
  gsap.from('.letter-content', {
    opacity: 0,
    y: 20,
    duration: 1,
    delay: 0.5
  });
});
</script>

<template>
  <div class="flex items-center justify-center min-h-screen px-4 py-8">
    <div class="letter-container paper w-full max-w-2xl mx-auto p-8 md:p-12 rounded-lg text-left">
      <div class="letter-content text-primary text-lg whitespace-pre-line">
        {{ letterContent }}
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Additional paper styling */
.letter-container {
  transform-origin: center;
  color: #333;
  line-height: 1.6;
  max-height: 80vh;
  overflow-y: auto;
}
</style>