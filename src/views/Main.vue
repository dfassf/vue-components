

<template>
  <div class="container-wrapper">
    <vertical-motion 
      :texts="text"
    />
  </div>
</template>
<script setup>
import { ref, watch, computed, onMounted, onUnmounted, } from 'vue'
import VerticalMotion from './components/VerticalMotion.vue';

const text = [
  '올라가는',
  '텍스트',
  'going',
  'up',
]

</script>
<style scoped lang="scss">
  .container-wrapper {
    width: 100%;
    height: 100%;
    min-height: 200px;
    display: flex;
    align-items: center;
    justify-content: center;

}
</style>
