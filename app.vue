<template>
  <div class="min-h-screen bg-gray-50 flex items-center justify-center">
    <div class="text-center">
      <h1 class="text-6xl font-bold tracking-tight text-gray-900">
        <span class="inline-flex relative">
          <!-- Base text -->
          <span
            v-for="(char, index) in 'domin'"
            :key="`base-${index}`"
            class="char-animate"
            :style="{
              '--char-delay': `${index * 0.05}s`,
            }"
            >{{ char }}</span
          >

          <!-- Transitioning characters -->
          <span
            v-if="!showFinal"
            class="char-animate fade-out"
            :style="{
              '--char-delay': `${5 * 0.05}s`,
            }"
            >i</span
          >
          <span
            v-if="!showFinal"
            class="char-animate fade-out"
            :style="{
              '--char-delay': `${6 * 0.05}s`,
            }"
            >c</span
          >

          <!-- Final additions -->
          <template v-if="showFinal">
            <span class="period-slide">.inc</span>
          </template>
        </span>
      </h1>
      <div class="h-12 relative">
        <h2
          v-if="showConsulting"
          class="text-3xl font-medium text-gray-600 consulting-slide absolute w-full"
        >
          <span
            v-for="(char, index) in 'consulting'"
            :key="`sub-${index}`"
            class="char-animate"
            :style="{
              '--char-delay': `${index * 0.05}s`,
            }"
            >{{ char }}</span
          >
        </h2>
      </div>
    </div>
  </div>
</template>

<script setup>
const showFinal = ref(false);
const showConsulting = ref(false);

onMounted(() => {
  setTimeout(() => {
    showFinal.value = true;
    // Show consulting text 350ms after .inc appears
    setTimeout(() => {
      showConsulting.value = true;
    }, 350);
  }, 1250);
});
</script>

<style scoped>
.char-animate {
  display: inline-block;
  opacity: 0;
  animation: morphCharacter 0.5s ease-out forwards;
  animation-delay: var(--char-delay);
}

.fade-out {
  animation: morphCharacter 0.5s ease-out forwards var(--char-delay),
    fadeOut 0.5s ease-out forwards 2s;
}

.period-slide {
  opacity: 0;
  display: inline-block;
  animation: slideIn 0.5s ease-out forwards;
}

.consulting-slide {
  opacity: 0;
  animation: slideUp 0.5s ease-out forwards;
}

@keyframes morphCharacter {
  from {
    opacity: 0;
    transform: translateX(-4px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
    transform: translateX(0);
  }
  to {
    opacity: 0;
    transform: translateX(10px);
  }
}

@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(-10px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

@keyframes slideUp {
  from {
    opacity: 0;
    transform: translateY(10px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>
