<template>
  <h1 v-if="mode === 'text'">{{ quizObject.answer.text }}</h1>
  <h1 v-if="mode === 'character'">{{ quizObject.answer.character }}</h1>
  <div v-for="choice in quizObject.choices" :key="choice.text" @click="$emit('on-answer', choice.text)">
    <span v-if="mode === 'text'">{{ choice.character }}</span>
    <span v-if="mode === 'character'">{{ choice.text }}</span>
  </div>
</template>

<script>

export default {
  name: "QuizCards",
  emits: ["on-answer"],
  props: {
    quizObject: Object,
    mode: String
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
