<template>
  <div class="h-full text-xl bg-white flex flex-col justify-center">
    <div>How Many Quiz Items?</div>
    <div>
      <input type="text" v-model="currentQuizCount"
             class="w-32 p-2 m-2 text-center border border-blue-500 rounded"
      />
    </div>
    <div>
      <input type="button" value="Start!"
             class="rounded bg-blue-500 text-3xl text-white px-10 py-2 my-8 cursor-pointer transition duration-200 ease-in-out hover:bg-blue-700 transform hover:-translate-y-1"
             @click="$emit('update:quizCount', currentQuizCount)"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "StartScreen",
  props: {
    quizCount: Number
  },
  emits: ["update:quizCount"],
  data() {
    return {
      currentQuizCount: this.quizCount
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
