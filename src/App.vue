<template>
  <h1>Reaction Timer</h1>
  <button @click="start" :disabled="state.isPlaying">Play</button>
  <Block 
    v-if="state.isPlaying" 
    :delay="state.delay" 
    @end="endGame"
  />
  <Results 
    v-if="state.showResults"
    :score="state.score"
  />
</template>

<script setup lang="ts">
import { reactive } from 'vue'
import Block from '@/components/Block.vue'
import Results from '@/components/Results.vue'

interface State {
  isPlaying: boolean
  delay: number | null
  score: number | null
  showResults: boolean
}

const state = reactive<State>({
  isPlaying: false,
  delay: null,
  score: null,
  showResults: false
})

function start () {
  state.isPlaying = true
  state.delay = 2000 + Math.random() * 5000
  state.showResults = false
}

function endGame (reactionTime: number) {
  state.score = reactionTime
  state.isPlaying = false
  state.showResults = true
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

button {
  background: #739be6;
  color: white;
  border: none;
  padding: 8px 16px;
  border-radius: 4px;
  font-size: 16px;
  letter-spacing: 1px;
  cursor: pointer;
  margin: 10px;
}
button:disabled {
  opacity: 0.2;
  cursor: not-allowed;
}
</style>
