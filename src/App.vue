<template>
  <div id="app">
    <StartScreen v-if="!started" :quiz-count="quizCount" @update:quizCount="generateStack"></StartScreen>
    <FlashCards v-if="!started && !completed" :choices="currentItem"/>
    <EndScreen v-if="completed"></EndScreen>
  </div>
</template>

<script>
import StartScreen from "@/components/StartScreen";
import FlashCards from '@/components/FlashCards.vue'
import EndScreen from "@/components/EndScreen";
import hangeul from "@/data/hangeul";

export default {
  name: 'App',
  components: {
    StartScreen,
    FlashCards,
    EndScreen
  },
  data() {
    return {
      started: false,
      completed: false,
      currentItem: undefined,
      currentStack: [],
      quizCount: 10,
      score: 0,
      total: 0
    }
  },
  methods: {
    reset() {
      this.started = false;
      this.completed = false;
      this.currentItem = undefined;
      this.currentStack = [];
      this.score = 0;
      this.total = 0;
    },
    generateStack(quizCount) {
      this.quizCount = quizCount;
      this.currentStack = hangeul;
      this.generateNextItem();
      this.started = true;
    },
    generateNextItem() {
      if (this.currentStack.length === 0) {
        this.completed = true;
        return;
      }
      this.currentItem = this.currentStack.pop();
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
