<template>
  <div class="min-h-screen valentine-gradient flex items-center justify-center p-4 sm:p-6 lg:p-8">
    <div class="confetti-container" ref="confettiContainer"></div>
    
    <!-- Main Card -->
    <div class="bg-white rounded-3xl shadow-2xl p-6 sm:p-8 lg:p-10 w-full max-w-sm sm:max-w-md lg:max-w-lg relative overflow-hidden">
      <!-- Decorative hearts -->
      <div class="absolute top-4 right-4 text-pink-200 text-2xl heart-float">💕</div>
      <div class="absolute top-8 left-4 text-pink-200 text-xl heart-float" style="animation-delay: 1s;">💖</div>
      <div class="absolute bottom-4 right-8 text-pink-200 text-lg heart-float" style="animation-delay: 2s;">💗</div>
      
      <!-- Page 1: Name Input -->
      <div v-if="currentPage === 1" class="text-center space-y-4 sm:space-y-6">
        <div class="space-y-2">
          <h1 class="text-3xl sm:text-4xl font-bold text-valentine-pink animate-pulse-slow">Hi 💖</h1>
          <p class="text-gray-600 text-base sm:text-lg">Can I get your name?</p>
        </div>
        
        <div class="space-y-3 sm:space-y-4">
          <input 
            v-model="name"
            type="text" 
            placeholder="Your beautiful name here"
            class="w-full px-3 sm:px-4 py-2 sm:py-3 border-2 border-pink-200 rounded-xl focus:outline-none focus:border-valentine-pink transition-colors text-center text-sm sm:text-base"
            @keyup.enter="goToNext"
          >
          <button 
            @click="goToNext"
            :disabled="!name.trim()"
            class="w-full bg-valentine-pink text-white py-2 sm:py-3 px-4 sm:px-6 rounded-xl font-semibold hover:bg-pink-600 transition-all transform hover:scale-105 disabled:opacity-50 disabled:cursor-not-allowed text-sm sm:text-base"
          >
            Continue 💕
          </button>
        </div>
      </div>

      <!-- Page 2: Date & Preferences -->
      <div v-if="currentPage === 2" class="text-center space-y-4 sm:space-y-6">
        <div class="space-y-2">
          <h1 class="text-2xl sm:text-3xl font-bold text-valentine-pink">Hi {{ name }} 💖</h1>
          <p class="text-gray-600 text-base sm:text-lg">When are you free?</p>
        </div>
        
        <div class="space-y-3 sm:space-y-4">
          <div>
            <input 
              v-model="selectedDate"
              type="date" 
              class="w-full px-3 sm:px-4 py-2 sm:py-3 border-2 border-pink-200 rounded-xl focus:outline-none focus:border-valentine-pink transition-colors text-sm sm:text-base"
              @input="validateDate"
            >
            <p v-if="dateError" class="text-red-500 text-xs sm:text-sm mt-2">{{ dateError }}</p>
          </div>

          <div class="space-y-2">
            <p class="text-gray-600 text-sm sm:text-base">Pick your drink ☕</p>
            <select 
              v-model="selectedDrink"
              class="w-full px-3 sm:px-4 py-2 sm:py-3 border-2 border-pink-200 rounded-xl focus:outline-none focus:border-valentine-pink transition-colors text-sm sm:text-base"
            >
              <option>Coffee</option>
              <option>Tea</option>
              <option>I prefer making our own drinks</option>
            </select>
          </div>

          <div class="space-y-2">
            <p class="text-gray-600 text-sm sm:text-base">Pick your food 🍜</p>
            <select 
              v-model="selectedFood"
              class="w-full px-3 sm:px-4 py-2 sm:py-3 border-2 border-pink-200 rounded-xl focus:outline-none focus:border-valentine-pink transition-colors text-sm sm:text-base"
            >
              <option>Takoyaki</option>
              <option>Shawarma</option>
              <option>Ramen</option>
              <option>Lugaw Date</option>
              <option>Anything basta masaya tayo</option>
            </select>
          </div>

          <div class="relative h-24 sm:h-32">
            <button 
              @click="sayYes"
              class="absolute left-0 bottom-0 bg-valentine-pink text-white py-2 sm:py-3 px-6 sm:px-8 rounded-full font-semibold hover:bg-pink-600 transition-all transform hover:scale-105 shadow-lg z-10 text-sm sm:text-base"
            >
              Yes 💖
            </button>
            <button 
              ref="noButton"
              @mouseenter="moveNoButton"
              @click="moveNoButton"
              @touchstart="moveNoButton"
              class="fixed bg-white text-valentine-pink border-2 border-valentine-pink py-2 sm:py-3 px-6 sm:px-8 rounded-full font-semibold hover:bg-pink-50 transition-all shadow-lg z-50 text-sm sm:text-base"
              style="left: 50%; bottom: 100px; transform: translateX(-50%);"
            >
              No 😳
            </button>
          </div>
        </div>
      </div>

      <!-- Page 3: Success -->
      <div v-if="currentPage === 3" class="text-center space-y-4 sm:space-y-6">
        <div class="space-y-3 sm:space-y-4">
          <h1 class="text-3xl sm:text-4xl font-bold text-valentine-pink animate-bounce">YAYYYYY 🎉💘</h1>
          <p class="text-gray-600 text-base sm:text-lg">Thank you for saying YES 🥹</p>
          <p class="text-gray-600 text-sm sm:text-base">Kaya mag-msg mo na ko 💌</p>
        </div>
        
        <div class="space-y-3 sm:space-y-4">
          <div class="bg-pink-50 p-3 sm:p-4 rounded-xl">
            <p class="text-xs sm:text-sm text-gray-600">Your date details:</p>
            <p class="font-semibold text-valentine-pink text-sm sm:text-base">{{ formatDate(selectedDate) }}</p>
            <p class="text-xs sm:text-sm text-gray-600">{{ selectedDrink }} & {{ selectedFood }}</p>
          </div>
          
          <button 
            @click="openFacebook"
            class="w-full bg-valentine-pink text-white py-2 sm:py-3 px-4 sm:px-6 rounded-xl font-semibold hover:bg-pink-600 transition-all transform hover:scale-105 shadow-lg text-sm sm:text-base"
          >
            Open Messages 💕
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, nextTick } from 'vue'
import confetti from 'canvas-confetti'

export default {
  name: 'ValentineProposal',
  setup() {
    const currentPage = ref(1)
    const name = ref('')
    const selectedDate = ref('')
    const selectedDrink = ref('Coffee')
    const selectedFood = ref('Takoyaki')
    const dateError = ref('')
    const noButton = ref(null)
    const confettiContainer = ref(null)

    const goToNext = () => {
      if (!name.value.trim()) {
        return
      }
      currentPage.value = 2
    }

    const validateDate = () => {
      if (!selectedDate.value) {
        dateError.value = ''
        return
      }
      
      const d = new Date(selectedDate.value)
      if (!(d.getMonth() === 1 && d.getDate() === 14)) {
        dateError.value = 'Feb 14 lang pwede 😌💘'
        selectedDate.value = ''
      } else {
        dateError.value = ''
      }
    }

    const moveNoButton = () => {
      if (!noButton.value) return
      
      const button = noButton.value
      const viewportWidth = window.innerWidth
      const viewportHeight = window.innerHeight
      const buttonWidth = button.offsetWidth
      const buttonHeight = button.offsetHeight
      
      // Calculate random position within viewport with padding
      const padding = 20
      const maxX = viewportWidth - buttonWidth - padding
      const maxY = viewportHeight - buttonHeight - padding
      
      const randomX = Math.random() * maxX + padding
      const randomY = Math.random() * maxY + padding
      
      button.style.position = 'fixed'
      button.style.left = `${randomX}px`
      button.style.top = `${randomY}px`
      button.style.transform = 'none'
      button.style.transition = 'all 0.2s ease'
    }

    const sayYes = () => {
      launchConfetti()
      setTimeout(() => {
        currentPage.value = 3
      }, 500)
    }

    const launchConfetti = () => {
      const duration = 3000
      const animationEnd = Date.now() + duration
      const defaults = { startVelocity: 30, spread: 360, ticks: 60, zIndex: 0 }

      function randomInRange(min, max) {
        return Math.random() * (max - min) + min
      }

      const interval = setInterval(function() {
        const timeLeft = animationEnd - Date.now()

        if (timeLeft <= 0) {
          return clearInterval(interval)
        }

        const particleCount = 50 * (timeLeft / duration)
        
        confetti(Object.assign({}, defaults, {
          particleCount,
          origin: { x: randomInRange(0.1, 0.3), y: Math.random() - 0.2 }
        }))
        confetti(Object.assign({}, defaults, {
          particleCount,
          origin: { x: randomInRange(0.7, 0.9), y: Math.random() - 0.2 }
        }))
      }, 250)
    }

    const formatDate = (dateString) => {
      if (!dateString) return ''
      const date = new Date(dateString)
      return date.toLocaleDateString('en-US', { 
        weekday: 'long', 
        year: 'numeric', 
        month: 'long', 
        day: 'numeric' 
      })
    }

    const openFacebook = () => {
      window.open("https://www.messenger.com/e2ee/t/7692563247462328", "_blank")
    }

    return {
      currentPage,
      name,
      selectedDate,
      selectedDrink,
      selectedFood,
      dateError,
      noButton,
      confettiContainer,
      goToNext,
      validateDate,
      moveNoButton,
      sayYes,
      formatDate,
      openFacebook
    }
  }
}
</script>
