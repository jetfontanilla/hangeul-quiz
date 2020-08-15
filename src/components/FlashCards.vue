<template>
  <div v-for="choice in choices" :key="choice.text" @click="$emit('on-answer', choice.text)">{{ choice.character }}</div>
</template>

<script>
export default {
  name: 'FlashCards',
  emits: ['on-answer'],
  props: {
    choices: Array
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
