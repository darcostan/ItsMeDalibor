<template>
  <div class="block" v-show="showBlock" @click="stopTimer">
    click me
  </div>
</template>

<script lang="ts">
import { Options, prop, Vue } from "vue-class-component";
import { StopWatch } from 'stopwatch-node';

@Options({
  props: {
    delay: Number,
  },
})
export default class HelloWorld extends Vue {
  delay!: number;
  showBlock = false;
  timer = 0;
  reactionTime = 0;
  
  sw = new StopWatch('sw');

  mounted() {
    setTimeout(() => {
      this.showBlock = true
      this.startTimer()
    }, this.delay)
  };
  startTimer() {
      // start the timer, tick every 10ms
      this.sw.start('time');
    };
    stopTimer() {
      // stop the timer
      this.sw.stop();

      this.reactionTime = this.sw.getTask('time')?.timeMills ?? 0;
      this.$emit('end', this.reactionTime)
    };
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.block {
    width: 400px;
    border-radius: 20px;
    background:  #0faf87;;
    color: white;
    text-align: center;
    padding: 100px 0;
    margin: 40px auto;
  }
</style>