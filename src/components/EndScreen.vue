<template>
  <div class="h-full text-xl bg-white flex flex-col justify-center">
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
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
