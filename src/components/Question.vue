<template>
  <div class="hello">
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
.gradient-box {
  border: 1px solid white;
}
</style>
