<template>
  <div class="h-full flex flex-col align-stretch justify-between">
    <div class="quiz-main flex-grow flex flex-col align-center justify-center text-5xl font-bold align-center"
         :class="{'bg-correct': isCorrect, 'bg-incorrect': isIncorrect}"
    >
      {{ mode === "text" ? quizObject.answer.text : quizObject.answer.character }}
    </div>
    <div class="bg-blue-300 grid grid-cols-2 gap-3">
      <div v-for="choice in quizObject.choices"
           :key="choice.text"
           @click="selectAnswer(choice.text)"
           class="bg-white rounded cursor-pointer text-3xl p-3 transition duration-200 ease-in-out hover:-translate-y-1"
           :class="{
             'hover:bg-yellow-200 transform': !checked,
             'bg-green-300': isChoiceCorrect(choice.text),
             'bg-red-300': isChoiceIncorrect(choice.text)
           }"
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
    mode: String,
    checked: Boolean
  },
  data() {
    return {
      selectedAnswer: undefined
    };
  },
  methods: {
    selectAnswer(answer) {
      this.selectedAnswer = answer;
      this.$emit("on-answer", answer);
    },
    isChoiceCorrect(choiceText) {
      if (!this.checked) {
        return false;
      }
      return this.quizObject.answer.text === choiceText;
    },
    isChoiceIncorrect(choiceText) {
      if (!this.checked) {
        return false;
      }
      return this.selectedAnswer === choiceText && this.quizObject.answer.text !== choiceText;
    }
  },
  computed: {
    isCorrect() {
      return this.checked && this.selectedAnswer === this.quizObject.answer.text;
    },
    isIncorrect() {
      return this.checked && this.selectedAnswer !== this.quizObject.answer.text;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-correct {
  background: url("../assets/cat-happy.gif") no-repeat right bottom;
}
.bg-incorrect {
  background: url("../assets/cat-sad.gif") no-repeat right bottom;
}
.quiz-main {
  background-size: auto 35vh;
}
</style>
