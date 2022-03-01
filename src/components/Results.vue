<template>
  <p>Reaction time: {{ props.score }} </p>
  <p class="rank">{{ state.rank }}</p>
</template>

<script setup lang="ts">
import { onMounted, reactive } from "vue"

interface Props {
  score: number
}

const props = withDefaults(defineProps<Props>(), {
  score: 0
})

interface State {
  rank: string
}

const state = reactive<State>({rank: ''})

onMounted(() => {
  if (props.score < 250) {
    state.rank = 'Ninja Fingers'
  } else if (props.score < 400) {
    state.rank = 'Rapid Reflexes'
  } else {
    state.rank = 'Snail pace...'
  }
})

</script>

<style lang="scss" scoped>
.rank {
  font-size: 1.4em;
  color: #739be6;
  font-weight: bold;
}
</style>