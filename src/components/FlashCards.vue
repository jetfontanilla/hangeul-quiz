<template>
  <div v-for="item of items" :key="item.message">{{ item }}</div>
</template>

<script>
export default {
  name: 'FlashCards',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
