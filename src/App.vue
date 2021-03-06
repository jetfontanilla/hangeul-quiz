<template>
  <div id="app" class="w-full h-full md:w-1/2 mx-auto p-3 bg-blue-300 rounded">
    <StartScreen v-if="!started"
                 :quiz-count="quizCount"
                 @update:quizCount="generateStack"
    ></StartScreen>
    <QuizCards v-if="started && !completed && currentItem"
               :quiz-object="currentItem"
               :mode="mode"
               :checked="checked"
               @on-answer="onAnswer"
    ></QuizCards>
    <EndScreen v-if="completed"
               :score="score"
               :total="quizCount"
               @on-reset="reset"
    ></EndScreen>
  </div>
</template>

<script>
import StartScreen from "@/components/StartScreen";
import QuizCards from "@/components/QuizCards.vue";
import EndScreen from "@/components/EndScreen";
import hangeul from "@/data/hangeul";
import sample from "lodash-es/sample";
import filter from "lodash-es/filter";
import sampleSize from "lodash-es/sampleSize";
import map from "lodash-es/map";
import shuffle from "lodash-es/shuffle";

const DEFAULT_QUIZ_COUNT = 10;
const ANIMATION_DELAY = 1000;

export default {
  name: "App",
  components: {
    StartScreen,
    QuizCards,
    EndScreen
  },
  data() {
    return {
      started: false,
      completed: false,
      checked: false,
      currentItem: undefined,
      mode: undefined,
      currentStack: [],
      quizCount: DEFAULT_QUIZ_COUNT,
      score: 0
    };
  },
  methods: {
    reset() {
      this.started = false;
      this.completed = false;
      this.checked = false;
      this.currentItem = undefined;
      this.currentStack = [];
      this.score = 0;
    },
    generateStack(rawQuizCount) {
      let quizCount = parseInt(rawQuizCount);
      if (!quizCount || isNaN(quizCount) || quizCount <= 0) {
        quizCount = DEFAULT_QUIZ_COUNT;
      }
      this.quizCount = quizCount;
      this.currentStack = map(new Array(this.quizCount), function() {
        let answer = sample(hangeul);
        let choices = sampleSize(filter(hangeul, function(item) {
          return item.text !== answer.text;
        }), 3);
        choices.push(answer);

        return {
          answer: answer,
          choices: shuffle(choices)
        };
      });
      this.generateNextItem();
      this.started = true;
    },
    onAnswer(answerText) {
      if (this.checked) {
        return;
      }
      if (answerText === this.currentItem.answer.text) {
        this.score += 1;
      }
      this.checked = true;
      setTimeout(this.generateNextItem, ANIMATION_DELAY);
    },
    generateNextItem() {
      if (this.currentStack.length === 0) {
        this.completed = true;
        return;
      }
      this.checked = false;
      this.mode = sample(["text", "character"]);
      this.currentItem = this.currentStack.pop();
    }
  }
};
</script>

<style>
html, body {
  height: 100%;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  height: 100%;
}

@media (min-width: 768px) {
  body {
    padding: 5rem;
  }
}
</style>
