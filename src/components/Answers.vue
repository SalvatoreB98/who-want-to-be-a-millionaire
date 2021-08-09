<template>
  <div>
    <div class="answers-container">
      <div
        v-for="(answer, index) in answers"
        :key="index"
        class="answer-container"
      >
        <button
          @click="answerClick(index)"
          :value="index"
          class="answer gradient-box d-inline-block"
        >
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

.answer-container {
  width: 50%;
}
.answer-container,
.question {
  padding-top: 20px;
  &:nth-child(1),
  &:nth-child(3) {
    padding-right: 10px;
    &::before {
      display: inline-block;
      z-index: 0;
      transform: translateX(-100%);
      position: absolute;
      content: ' ';
      top: 57%;
      left: 0px;
      height: 10px;
      width: 10vw;
      border-top: 2px solid white;
    }
  }
  &:nth-child(2),
  &:nth-child(4) {
    padding-left: 10px;
  }
  position: relative;
  &::before {
    display: inline-block;
    z-index: 0;
    transform: translateX(-100%);
    position: absolute;
    content: ' ';
    top: 57%;
    left: 0px;
    height: 10px;
    width: 1vw;
    border-top: 2px solid white;
  }
  &::after {
    display: inline-block;
    z-index: 0;
    transform: translateX(100%);
    position: absolute;
    content: ' ';
    top: 57%;
    right: 1px;
    height: 10px;
    width: 10vw;
    border-top: 2px solid white;
  }
}
.answer {
  width: 100%;
  text-align: left;
  padding: 25px;
  cursor: pointer;
  &:hover {
    background: rgb(19, 17, 47);
  }
}
.gradient-box {
  z-index: 2;
  background: #050545;
  background: linear-gradient(
    0deg,
    #050545 50%,
     #06062c 90%,
  );
  border-radius: 7em 7em 7em / 7em 7em 7em;
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
  background: green;
  &:hover {
    background: green;
  }
}
.wrong {
  background: red;
  &:hover {
    background: red;
  }
}
.blinking {
  animation: blinking 0.5s infinite ease-in-out;
}
@keyframes blinking {
  0% {
    background: #fbcb2bfa;
  }
  50% {
    background: #050545;
  }
}
@media screen and (max-width: 720px) {
  .answer-container {
    width: 100%;
    padding-top: 20px;
    &:nth-child(1),
    &:nth-child(3) {
      padding-right: 10px;
      &::before {
        display: inline-block;
        z-index: 0;
        transform: translateX(-100%);
        position: absolute;
        content: ' ';
        top: 57%;
        left: 0px;
        height: 10px;
        width: 10vw;
        border-top: 2px solid white;
      }
    }
    &:nth-child(2),
    &:nth-child(4) {
      padding-left: 10px;
    }
    position: relative;
    &::before {
       display: inline-block;
        z-index: 0;
        transform: translateX(-100%);
        position: absolute;
        content: ' ';
        top: 57%;
        left: 0px;
        height: 10px;
        width: 10vw;
        border-top: 2px solid white;
    }
    &::after {
      display: inline-block;
      z-index: 0;
      transform: translateX(100%);
      position: absolute;
      content: ' ';
      top: 57%;
      right: 1px;
      height: 10px;
      width: 10vw;
      border-top: 2px solid white;
    }
  }
}
</style>
