<template>
  <div>Your Score: {{ score }} / {{ total }}</div>
  <input type="button" value="Try Again?" @click="$emit('on-reset')" />
</template>

<script>
export default {
  name: 'EndScreen',
  emits: ['on-reset'],
  props: {
    score: Number,
    total: Number
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
