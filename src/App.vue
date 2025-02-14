<script setup>
import { ref } from 'vue'

const isClicked = ref(false)

const handleClick = () => {
  isClicked.value = !isClicked.value
}
</script>

<template>
  <div
    class="flex justify-center items-center h-screen relative bg-gradient-to-r from-pink-400 via-red-500 to-yellow-500"
  >
    <!-- ข้อความ Happy Valentine Day อยู่ข้างหลังหัวใจ -->
    <div
      class="absolute text-0xl font-extrabold text-white drop-shadow-lg p-4 rounded-lg z-0 transition-transform duration-700 ease-in-out"
      :class="{ '-translate-y-80': isClicked, 'text-3xl': isClicked }"
    >
      Happy Valentine’s Day 💖
    </div>

    <!-- รูปหัวใจ -->
    <img
      src="./assets/heart.png"
      alt="heart"
      class="transition-transform duration-500 transform hover:scale-125 cursor-pointer animate-bounce-slow"
      @click="handleClick"
      :class="{
        'w-40': isClicked,
        'animate-bounce-slow': isClicked,
      }"
    />
  </div>

  <!-- รูป S1 และ S2 ที่อยู่กลางจอ -->
  <TransitionGroup name="fade">
    <div
      v-if="isClicked"
      class="absolute inset-0 flex justify-center items-center gap-40"
    >
      <img
        src="./assets/S1.png"
        class="w-72 h-72 object-contain drop-shadow-[0_10px_30px_rgba(0,0,0,0.3)] animate-rotate-pop brightness-110"
      />
      <img
        src="./assets/S2.png"
        class="w-72 h-72 object-contain drop-shadow-[0_10px_30px_rgba(0,0,0,0.3)] animate-rotate-pop brightness-110"
      />
    </div>
  </TransitionGroup>
</template>

<style scoped>
/* เอฟเฟกต์ fade in */
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.8s ease-out, transform 0.8s ease-out;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: scale(0.5);
}

/* เอฟเฟกต์เด้งออกมา */
@keyframes pop {
  0% {
    transform: scale(0.5);
    opacity: 0;
  }
  50% {
    transform: scale(1.1);
    opacity: 1;
  }
  100% {
    transform: scale(1);
  }
}

.animate-pop {
  animation: pop 0.6s ease-out forwards;
}
@keyframes bounce-slow {
  0%,
  100% {
    transform: scale(1);
  }
  50% {
    transform: scale(1.1);
  }
}

.animate-bounce-slow {
  animation: bounce-slow 1.5s infinite ease-in-out;
}
</style>
