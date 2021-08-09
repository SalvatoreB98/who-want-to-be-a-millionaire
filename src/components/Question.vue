<template>
  <div>
    <h1 class="question gradient-box">{{ question }}</h1>
  </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
    question: String,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
.question{
  padding: 25px;
}
</style>
