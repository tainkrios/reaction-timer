<template>
  <h1>Reaction Timer</h1>
  <button @click="start" :disabled="state.isPlaying">Play</button>
  <Block 
    v-if="state.isPlaying" 
    :delay="state.delay" 
    @end="endGame"
  />
  <p>Reaction time: {{ state.score }}</p>
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import Block from '@/components/Block.vue'

interface State {
  isPlaying: boolean
  delay: number | null
  score: number | null
}

const state = reactive<State>({
  isPlaying: false,
  delay: null,
  score: null
})

function start () {
  state.isPlaying = true
  state.delay = 2000 + Math.random() * 5000
}

function endGame (reactionTime: number) {
  state.score = reactionTime
  state.isPlaying = false
}

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #444;
  margin-top: 60px;
}
</style>
