<template>
  How Many Items?
  <input type="text" v-model="currentQuizCount" />
  <input type="button" value="Submit" @click="$emit('update:quizCount', currentQuizCount)" />

</template>

<script>
export default {
  name: 'StartScreen',
  props: {
    quizCount: Number
  },
  emits: ['update:quizCount'],
  data() {
    return {
      currentQuizCount: this.quizCount
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
