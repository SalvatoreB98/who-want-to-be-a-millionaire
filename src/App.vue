<template>
  <div id="app">
    <div v-if="!gameOver" class="d-flex my-layout-container">
      <div
        class="p-5 flex-grow-1 content-container"
        :class="gameOver ? 'game-over' : ''"
      >
        <div class="logo-container">
          <div style="position: absolute; top: 0; left: 0">
            <i class="fa fa-user" aria-hidden="true"></i> {{ name }}
          </div>
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
    <div v-if="gameOver" class="gif-container">
      <img
        src="https://acegif.com/wp-content/gif/confetti-10.gif"
        class=""
        alt=""
      />
    </div>
    <div v-if="gameOver" class="recap">
      <h1>Results:</h1>
      <h3>{{ name }}</h3>
      <h3>You have won: {{ record }}€</h3>
      <h1 class="text-white">
        <button @click="play()" class="btn btn-light" style="min-width: 300px">
          PLAY AGAIN
        </button>
      </h1>
    </div>
    <div
      v-if="!isStarted"
      class="popup d-flex justify-content-center align-items-center flex-column"
    >
      <div class="logo-container p-1">
        <img
          class="logo"
          alt="Vue logo"
          src="./assets/logo.png"
          style="min-width: 300px"
        />
      </div>
      <div class="form-group m-3">
        <label for=""
          >Insert your name <br />
          <input class="form-text mt-3" type="text" v-model="name" />
        </label>
      </div>
      <h1 class="text-white">
        <button @click="play()" class="btn btn-light" style="min-width: 300px">
          PLAY
        </button>
      </h1>
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
      name: '',
      myData: json,
      currentQuestion: '',
      answers: [],
      activePrize: 0,
      animationCorrect: false,
      isStarted: false,
      gameOver: false,
      record: 0,
    }
  },
  mounted() {},
  methods: {
    play() {
      this.gameOver = false
      this.isStarted = true
      this.randomQuestion()
    },
    clicked(value) {
      console.log('La risposta è...')
      if (value == this.currentQuestion.correct) {
        setTimeout(() => {
          this.record = this.myData.prizes[this.activePrize]
          this.animationCorrect = true
          console.log('CORRETTA')
          var prizesBar = document.querySelector('.climbing-container')
          prizesBar.classList.add('open-menu')
          setTimeout(() => {
            this.activePrize += 1
            this.animationCorrect = false
            setTimeout(() => {
              this.randomQuestion()
              prizesBar.classList.remove('open-menu')
            }, 1500)
          }, 1500)
        }, 3000)
      } else {
        setTimeout(() => {
          console.log('SBAGLIATA')
          var prizesBar = document.querySelector('.climbing-container')
          prizesBar.classList.add('open-menu')
          setTimeout(() => {
            this.gameOver = true
            this.activePrize = 0
            setTimeout(() => {
              this.randomQuestion()
              prizesBar.classList.remove('open-menu')
            }, 1500)
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
  position: relative;
  padding: 35px;
}
.climbing-container {
  padding: 25px;
  z-index: 3;
  border-left: 5px solid lightblue;
  background-color: #050545;
  width: 200px;
  transition: width 1s cubic-bezier(0.075, 0.82, 0.165, 1);
}
.gif-container {
  transition: all;
  position: absolute;
  top: 0;
  width: 100vw;
  height: 100vh;
  img {
    width: 100%;
    height: 100%;
    object-fit: cover;
  }
  animation: entrance 2s ease-in-out;
}
.popup {
  background-image: url('https://i.ytimg.com/vi/7mq7wXH8hNo/maxresdefault.jpg');
  background-repeat: no-repeat;
  background-size: cover;
  width: 100vw;
  height: 100vh;
  z-index: 6;
  transition: all;
  position: absolute;
  top: 0;
}
input[type='text'] {
  background: none;
  border-radius: 5em 5em 5em;
  border: 1px solid white;
  min-width: 300px;
  color: white;
  text-align: center;
}
.recap {
  z-index: 10;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
.game-over {
  animation: game-over 6s cubic-bezier(0.075, 0.82, 0.165, 1) alternate-reverse;
}
.content-container {
  transition: transform 1s ease-in-out;
}
@keyframes entrance {
  0% {
    opacity: 0;
  }
  10% {
    opacity: 100%;
  }
  90% {
    opacity: 100%;
  }
  100% {
    opacity: 0;
  }
}
@keyframes game-over {
  0% {
    opacity: 100%;
  }
  100% {
    opacity: 0%;
  }
}
.open-menu {
  width: 500px;
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
