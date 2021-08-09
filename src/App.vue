<template>
  <div id="app">
    <div class="d-flex my-layout-container">
      <div class="p-5 flex-grow-1">
        <div class="logo-container">
          <img class="logo" alt="Vue logo" src="./assets/logo.png" />
        </div>

        <question :question="currentQuestion.question" />
        <answers
          @clicked="clicked"
          :answers="currentQuestion.content"
          :correct="currentQuestion.correct"
        />
      </div>
      <div class="climbing-container">
        <climbing :prizes="myData.prizes" :activePrize="activePrize" />
      </div>
    </div>
    <div v-if="animationCorrect" class="gif-container">
      <!-- https://acegif.com/wp-content/gif/confetti-10.gif -->
      <img
        src="./assets/check.gif"
        class=""
        alt=""
      />
    </div>
  </div>
</template>

<script>
import Answers from './components/Answers.vue'
import Climbing from './components/Climbing.vue'
import question from './components/Question.vue'
import json from './data.json'
export default {
  name: 'App',
  components: {
    question,
    Answers,
    Climbing,
  },
  data() {
    return {
      myData: json,
      currentQuestion: '',
      answers: [],
      activePrize: 0,
      animationCorrect: false,
    }
  },
  mounted() {
    this.randomQuestion()
  },
  methods: {
    clicked(value) {
      console.log('La risposta è...')
      if (value == this.currentQuestion.correct) {
        setTimeout(() => {
          this.animationCorrect = true
          console.log('CORRETTA')
          setTimeout(() => {
            this.activePrize += 1
            this.randomQuestion()
            this.animationCorrect = false
          }, 1500)
        }, 3000)
      } else {
        setTimeout(() => {
          console.log('SBAGLIATA')
          setTimeout(() => {
            this.activePrize = 0
            this.randomQuestion()
          }, 1500)
        }, 3000)
      }
    },
    randomQuestion() {
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
  },
}
</script>

<style lang="scss">
html {
  height: 100vh;
  background-image: url('https://i.ytimg.com/vi/7mq7wXH8hNo/maxresdefault.jpg');
  overflow-x: hidden;
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
  background-image: url('https://i.ytimg.com/vi/7mq7wXH8hNo/maxresdefault.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  color: white;
}
.my-layout-container {
  height: 100vh;
}
.logo {
  width: 200px;
}
.logo-container {
  padding: 35px;
}
.climbing-container {
  padding: 25px;
  z-index: 3;
  border-left: 5px solid lightblue;
  background-color: #050545;
}
.gif-container {
  z-index: 6;
  transition: all;
  position: absolute;
  top: 0;
  img {
    width: 100vw;
    height: 100vh;
    object-fit: cover;
  }
  animation: entrance 1.5s 1 ease-in-out;
}
@keyframes entrance {
  0% {
    opacity: 0;
  }
  50% {
    opacity: 100%;
  }
  100%{
    opacity: 0;
  }
}
@media screen and(max-width:725px) {
  .logo {
    width: 50px;
  }
  .logo-container {
    padding: 10px;
  }
}
</style>
