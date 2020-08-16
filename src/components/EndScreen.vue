<template>
  <div class="end-main h-full text-xl bg-white flex flex-col justify-center"
       :class="{
          'bg-success': scorePercentage > 0.7,
          'bg-passed': scorePercentage > 0.4 && scorePercentage <= 0.7,
          'bg-fail': scorePercentage <= 0.4
       }"
  >
    <div>Your Score: {{ score }} / {{ total }}</div>
    <div>
      <input @click="$emit('on-reset')"
             type="button"
             value="Try Again?"
             class="rounded bg-blue-500 text-3xl text-white px-10 py-2 my-8 cursor-pointer transition duration-200 ease-in-out hover:bg-blue-700 transform hover:-translate-y-1"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "EndScreen",
  emits: ["on-reset"],
  props: {
    score: Number,
    total: Number
  },
  computed: {
    scorePercentage() {
      return this.total > 0 ? this.score / this.total : 0;
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.bg-success {
  background: #fff url("../assets/cat-success.gif") no-repeat right bottom;
}
.bg-passed {
  background: #fff url("../assets/cat-passed.gif") no-repeat right bottom;
}
.bg-fail {
  background: #fff url("../assets/cat-fail.gif") no-repeat right bottom;
}
.end-main {
  background-size: auto 40vh;
}
</style>
