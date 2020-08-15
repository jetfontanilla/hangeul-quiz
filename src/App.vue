<template>
  <div id="app">
    <StartScreen></StartScreen>
    <FlashCards msg="Welcome to Your Vue.js App"/>
    <EndScreen></EndScreen>
  </div>
</template>

<script>
import StartScreen from "@/components/StartScreen";
import FlashCards from '@/components/FlashCards.vue'
import EndScreen from "@/components/EndScreen";

export default {
  name: 'App',
  components: {
    StartScreen,
    FlashCards,
    EndScreen
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
