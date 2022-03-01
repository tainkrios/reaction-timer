<template>
  <div 
    class="block" 
    v-if="state.showBlock"
    @click="stopTimer"
  >
    click me
  </div>
</template>

<script setup lang="ts">
import { defineProps, onMounted, withDefaults, reactive } from 'vue'

interface State {
  showBlock: boolean
  timer: number | undefined | null
  reactionTime: number
}

const state = reactive<State>(
  {
    showBlock: false,
    timer: null,
    reactionTime: 0
  }
)

interface Props {
  delay: number
}

const props = withDefaults(defineProps<Props>(), {
  delay: 0
})

const emit = defineEmits<{
  (e: 'end', value: number): void
}>()

onMounted(() => {
  setTimeout(() => {
    state.showBlock = true
    startTimer()
  }, props.delay)
})

function startTimer () {
  state.timer = setInterval(() => {
    state.reactionTime += 10
  }, 10)
}

function stopTimer () {
  clearInterval(state.timer)
  emit('end', state.reactionTime)
}

</script>

<style scoped lang="scss">
  .block {
    width: 400px;
    border-radius: 20px;
    background: #739be6;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
  }
</style>