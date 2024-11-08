<template>
  <div class="min-h-screen bg-gray-50 flex items-center justify-center">
    <!-- Gradient background -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="wave-gradient"></div>
    </div>

    <div class="relative z-10">
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
.wave-gradient {
  position: absolute;
  width: 100%;
  height: 100%;
  top: -50%;
  left: -50%;
  background: radial-gradient(circle at center, 
    rgba(139, 92, 246, 0.15) 0%,
    rgba(59, 130, 246, 0.15) 25%,
    rgba(236, 72, 153, 0.15) 50%,
    rgba(139, 92, 246, 0.15) 75%,
    rgba(59, 130, 246, 0.15) 100%
  );
  filter: blur(40px);
  animation: rotate 20s linear infinite;
  transform-origin: center center;
}

.wave-gradient::after {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(circle at center,
    transparent 0%,
    rgba(255, 255, 255, 0.8) 70%
  );
}

@keyframes rotate {
  from {
    transform: rotate(0deg);
  }
  to {
    transform: rotate(360deg);
  }
}

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
