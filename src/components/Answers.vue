<template>
  <div class="hello">
    <div class="answers-container">
      <div v-for="(answer, index) in answers" :key="index" style="width:50%" class="answer-container">
        <button
          @click="answerClick(index)"
          :value="index"
          class="answer gradient-box d-inline-block">
          <span> &#8226;</span>
          <span v-if="index == 0" class="letter"> A: </span>
          <span v-if="index == 1" class="letter"> B: </span>
          <span v-if="index == 2" class="letter"> C: </span>
          <span v-if="index == 3" class="letter"> D: </span>
          {{ answer }}
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Answers',
  props: {
    correct: Number,
    answers: Array,
  },
  data() {
    return {
      isAnswered: false,
      isCorrect: null,
      answered: null,
    }
  },
  methods: {
    answerClick(index) {
      if (!this.isAnswered) {
        var clickedElement = document.querySelector(`button[value='${index}']`)
        clickedElement.classList.add('blinking')
        setTimeout(() => {
          clickedElement.classList.remove('blinking')
          if (index == this.correct) {
            this.isCorrect = true
            clickedElement.classList.add('correct')
          } else {
            this.isCorrect = false
            clickedElement.classList.add('wrong')
          }
        }, 3000)
        this.answered = index
        this.isAnswered = true
        this.$emit('clicked', index)
      }
    },
  },
}
</script>


<!-- STYLE -->
<style lang="scss" >
.answers-container {
  justify-content: center;
  display: flex;
  flex-wrap: wrap;
}
.answer-container{
  padding-top: 20px;
  &:nth-child(1),&:nth-child(3){
    padding-right: 10px;
  }
   &:nth-child(2),&:nth-child(4){
    padding-left: 10px;
  }
}
.answer {
  width: 100%;
  text-align: left;
  padding: 25px;
  cursor: pointer;
  &:hover {
    background-color: rgb(19, 17, 47);
  }
}
.gradient-box {
  border-top-left-radius: 0%;
  border: 2px solid white;
}
h2 {
  margin: 10px;
}
.letter {
  color: #fa9317;
}
button {
  border: none;
  margin: 0;
  padding: 0;
  width: auto;
  overflow: visible;

  background: transparent;

  /* inherit font & color from ancestor */
  color: inherit;
  font: inherit;

  /* Normalize `line-height`. Cannot be changed from `normal` in Firefox 4+. */
  line-height: normal;

  /* Corrects font smoothing for webkit */
  -webkit-font-smoothing: inherit;
  -moz-osx-font-smoothing: inherit;

  /* Corrects inability to style clickable `input` types in iOS */
  -webkit-appearance: none;
}
.correct {
  background-color: green;
  &:hover {
    background-color: green;
  }
}
.wrong {
  background-color: red;
  &:hover {
    background-color: red;
  }
}
.blinking {
  animation: blinking 0.5s infinite ease-in-out;
}
@keyframes blinking {
  0% {
    background-color: #fbcb2bfa;
  }
  50% {
    background-color: #050545;
  }
}
@media screen and (max-width: 720px) {
  
}
</style>
