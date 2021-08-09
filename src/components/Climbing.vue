<template>
  <div>
    <ol class="d-flex flex-column-reverse">
      <li
        class="text-start p-1 gradient-box text-center m-1"
        v-for="(prize, index) in prizes"
        :key="index"
      >
        <button
          :class="index % 5 == 0 || index == 14 ? '' : 'important'"
          style="cursor: auto"
          value="index"
        >
          <span :class="activePrize == index ? 'active' : ''">
            {{ prize }}
          </span>
        </button>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: 'Question',
  props: {
    activePrize: Number,
    prizes: Array,
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>
span {
  display: inline-block;
  width: 100%;
  text-align: center;
  transition: all 1s cubic-bezier(0.075, 0.82, 0.165, 1);
}
ol {
  li {
    font-weight: bold;
    button {
      width: 100%;
      text-align: center;
    }
  }
}

.important {
  color: #fa9317;
}
.active {
  border-radius: 5em 5em 5em;
  display: inline-block;
  padding: 5px;
  font-size: 1.2em;
  background: #fa9317;
  color: white;
  &::after {
    margin-left: 5px;
    color: white;
    display: inline-block;
    transform: scale(1.7);
    content: '\2022';
  }
}
</style>