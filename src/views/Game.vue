<template>
  <h1>Ninja Reaction Timer</h1>
  <button @click="start" :disabled="isPlaying">play</button>
  <Block v-if="isPlaying" :delay="delay" @end="endGame" />
  <p v-if="showResults">Reaction time: {{ score }} ms</p>
</template>

<script lang="ts">
import { Options, Vue } from "vue-class-component";
import Block from "../components/Block.vue"

@Options({
  components: {
      Block
  },
})
export default class Game extends Vue {
    isPlaying = false;
    delay = 0;
    score = 0;
    showResults = false;

    start() {
      // set time amount (ms)
      this.delay = 2000 + Math.random() * 5000
      this.isPlaying = true
      this.showResults = false
    };
    endGame(reactionTime: number) {
      this.score = reactionTime
      this.isPlaying = false
      this.showResults = true
    };
}
</script>
