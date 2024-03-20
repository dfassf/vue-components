<template>
  <div class="text-container" :style="{ width, height }">
    <span :key="animationKey" class="text animate" :style="textStyle">
      {{ currentText }}
    </span>
  </div>
</template>

<script setup>
import { ref, watch, computed, onMounted, onUnmounted, } from 'vue'




// Define props
const props = defineProps({
  texts: Array,
  width: {
    type: String,
    default: '100%' // Example default value
  },
  height: {
    type: String,
    default: '60px' // Example default value
  },
  fontSize: {
    type: String,
    default: '30px' // Example default value
  },
  animateSecond: {
    type: Number,
    default: 0.5 // In seconds
  },
  interval: {
    type: Number,
    default: 1000 // In milliseconds
  }
})


const currentText = ref(props.texts[0])
let index = 0
const animationKey = ref(0)

// Interval for changing text
let intervalId = null

onMounted(() => {
  intervalId = setInterval(() => {
    index = (index + 1) % props.texts.length
    currentText.value = props.texts[index]
    animationKey.value++ // Increment key to restart the animation
  }, props.interval)
})

onUnmounted(() => {
  if (intervalId !== null) {
    clearInterval(intervalId)
  }
})

// Dynamic style for the text
const textStyle = computed(() => ({
  fontSize: props.fontSize,
  animationDuration: `${props.animateSecond}s`
}))
</script>
<style scoped lang="scss">
  .container-wrapper {
    width: 100%;
    height: 100%;
    min-height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;
    .text-container {
      width: 300px;
      height: 60px;
      display: flex;
      align-items: center;
      position: relative;
      overflow: hidden;
      .text {
        font-size: 30px;
        position: absolute;
        top: 0px;
      }
    }


    .animate {
      animation: moveUp 0.5s ease-in-out forwards;
    }

    @keyframes moveUp {
      0% {
        top: 0px;
      }
      50% {
        top: 0px;
      }
      100% {
        top: -40px;
        filter: blur(2px);
      }
    }

}
</style>
