<template>
  <div class="p-5" id="app">
    <div class="p-5">
      <img alt="Vue logo" src="./assets/logo.png" />
    </div>

    <question :question="currentQuestion.question"/>
    <answers
      @clicked="clicked"
      :answers="currentQuestion.content"
      :correct="currentQuestion.correct"
    />
  </div>
</template>

<script>
import Answers from './components/Answers.vue'
import question from './components/Question.vue'
import json from './data.json'
export default {
  name: 'App',
  components: {
    question,
    Answers,
  },
  data() {
    return {
      myData: json,
      currentQuestion: '',
      answers: [],
    }
  },
  mounted() {
    let randomQuestionGroup = Math.floor(Math.random() * 5)
    let randomQuestion = Math.floor(
      Math.random() * this.myData.games[randomQuestionGroup].questions.length
    )
    console.log(
      this.myData.games[randomQuestionGroup].questions[randomQuestion]
    )
    this.currentQuestion =
      this.myData.games[randomQuestionGroup].questions[randomQuestion]
  },
  methods: {
    clicked(value) {
      if (value == this.currentQuestion.correct) {
        console.log('CORRETTA')
      } else {
        console.log('SBAGLIATA')
      }
    },
  },
}
</script>

<style lang="scss">
html {
  height: 100vh;
  background-color: #050545;
}
body {
  margin: 0;
}
#app {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #050545;
  color: white;
  padding: 25px;
}
</style>
