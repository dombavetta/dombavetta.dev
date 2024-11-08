<template>
  <div class="max-w-screen min-h-screen bg-gray-50 flex items-center justify-center overflow-hidden">
    <!-- Gradient background -->
    <div class="absolute inset-0 overflow-hidden">
      <div class="wave-gradient top"></div>
      <div class="wave-gradient bottom"></div>
    </div>

    <!-- <div
      class="roll absolute bottom-0 left-0 bg-white bg-opacity-40 rounded-full border-4 border-[#eed0d0] overflow-hidden"
      :style="{
        '--travel-time': '3s',
        '--spin-rate': '650ms'
      }"
      >
      <img src="~/assets/images/me.png" alt="Doms Avator, hes appears handsome 🙂" class="spin h-[80px]" />
    </div> -->

    <!-- Heading -->
    <div class="relative z-10">
      <div class="text-center">
        <h1 class="text-6xl font-bold tracking-tight text-gray-900">
          <!-- Main - domin.inc -->
          <span class="inline-flex relative">
            <!-- Base text - "domin" -->
            <span
              v-for="(char, index) in 'domin'"
              :key="`base-${index}`"
              class="char char-animate"
              :style="{
                '--char-delay': `${index * 0.05}s`,
              }"
              >{{ char }}</span
            >

            <!-- Transition out - "ic" -->
            <span
              v-if="!showInc"
              class="char char-animate fade-out"
              :style="{ '--char-delay': `${5 * 0.05}s` }"
              >i</span
            >
            <span
              v-if="!showInc"
              class="char char-animate fade-out"
              :style="{ '--char-delay': `${6 * 0.05}s` }"
              >c</span
            >

            <!-- Transition in - ".inc" -->
            <template v-if="showInc">
              <span
                v-for="(char, index) in '.inc'"
                :key="`sub-${index}`"
                class="char char-slide-down"
                :style="{ '--char-delay': `${index * 0.05}s` }"
                >{{ char }}</span
              >
            </template>
          </span>
        </h1>
        <!-- Subheading - "consulting" -->
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
const showInc = ref(false);
const showConsulting = ref(false);

onMounted(() => {
  setTimeout(() => {
    showInc.value = true;
    // Show "consulting" text 350ms after .inc appears
    setTimeout(() => (showConsulting.value = true), 350);
  }, 1250);
});
</script>

<style scoped>
.wave-gradient {
  position: absolute;
  width: 100%;
  height: 100%;
  filter: blur(40px);
  animation: rotate 20s linear infinite;
  transform-origin: center center;
}

.wave-gradient.top {
  top: -50%;
  left: -50%;
  background: radial-gradient(circle at center, 
    rgba(139, 92, 246, 0.15) 0%,
    rgba(59, 130, 246, 0.15) 25%,
    rgba(236, 72, 153, 0.15) 50%,
    rgba(139, 92, 246, 0.15) 75%,
    rgba(59, 130, 246, 0.15) 100%
  );
}

.wave-gradient.bottom {
  top: 50%;
  left: 50%;
  background: radial-gradient(circle at center, 
    rgba(205, 92, 246, 0.15) 0%,
    rgba(59, 159, 246, 0.15) 25%,
    rgba(72, 236, 159, 0.15) 50%,
    rgba(246, 244, 92, 0.15) 75%,
    rgba(246, 106, 59, 0.15) 100%
  );
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

.roll {
  animation: roll var(--travel-time) linear forwards;
}

.spin {
  animation: spin var(--spin-rate) linear infinite;
}

@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

@keyframes roll {
  0% {
    transform: translateX(-100%);
  }
  100% {
    transform: translateX(100vw);
  }
}

.char {
  display: inline-block;
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

.consulting-slide {
  opacity: 0;
  animation: slideUp 0.5s ease-out forwards;
}

.char-slide-down {
  opacity: 0;
  animation: slideDown 0.5s ease-out forwards;
  animation-delay: var(--char-delay);
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

@keyframes slideDown {
  from {
    opacity: 0;
    transform: translateY(-20px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
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
