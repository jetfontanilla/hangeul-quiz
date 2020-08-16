<template>
  <div class="h-full flex flex-col align-stretch justify-between">
    <div class="flex-grow flex flex-col align-center justify-center text-5xl font-bold align-center">
      {{ mode === 'text' ? quizObject.answer.text : quizObject.answer.character }}
    </div>
    <div class="bg-blue-300 grid grid-cols-2 gap-3">
      <div v-for="choice in quizObject.choices"
           :key="choice.text"
           @click="$emit('on-answer', choice.text)"
           class="bg-white rounded cursor-pointer text-3xl p-3 transition duration-200 ease-in-out hover:bg-yellow-200 transform hover:-translate-y-1"
      >
        <span v-if="mode === 'text'">{{ choice.character }}</span>
        <span v-if="mode === 'character'">{{ choice.text }}</span>
      </div>
    </div>
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
