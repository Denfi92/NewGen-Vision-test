<template>
  <main class="main container z-depth-5">
    <typing-test
      :text="text"
      :step="step"
      :time="time"
      :uncorrectChar="uncorrectChar"
      :testStarted="testStarted"
    ></typing-test>
    <typing-repeat
      :testStarted="testStarted"
      @repeatTest="repeatTest"
      :testOver="testOver"
    ></typing-repeat>
    <typing-result
      v-if="testOver"
      :speed="speed"
      :accuracity="accuracity"
    ></typing-result>
  </main>
</template>

<script>
import TypingResult from './TypingResult.vue';
import TypingRepeat from './TypingRepeat.vue';
import TypingTest from './TypingTest.vue';

export default {
  name: 'TypingArea',
  data() {
    return {
      text: ' ',
      key: undefined,
      testStarted: false,
      uncorrectChar: false,
      testOver: false,
      speed: 0,
      step: 0,
      accuracity: 0,
      timer: 0,
      time: 0,
      uncorrectCount: 0,
      isExeption: ['Shift', 'Control', 'Escape', 'Enter'],
    };
  },
  components: {
    TypingResult,
    TypingRepeat,
    TypingTest,
  },
  methods: {
    async fetchText() {
      const response = await fetch(
        'https://baconipsum.com/api/?type=all-meat&sentences=1&start-with-lorem=1',
      );
      const res = await response.json();
      this.text = res.join();
    },
    endTest() {
      this.testOver = true;
      clearInterval(this.timer);
    },
    repeatTest() {
      this.testOver = false;
      this.fetchText();
      this.step = 0;
      clearInterval(this.timer);
      this.testStarted = false;
      this.time = 0;
      this.accuracity = 0;
      this.speed = 0;
      this.uncorrectCount = 0;
    },
    handlePress(e) {
      this.key = e.key;
      if (!this.isExeptionKey(this.key)) {
        if (this.compareChar(this.key)) {
          this.uncorrectChar = false;
          this.nextStep();
          if (this.step === 1) {
            this.startTest();
          }
        } else {
          this.uncorrectCount += 1;
          this.uncorrectChar = true;
        }
      }
    },
    compareChar(char) {
      if (this.step < this.text.length - 1) {
        const correct = this.text[this.step];
        if (correct === char) {
          return true;
        }
        return false;
      }
      return this.endTest();
    },
    nextStep() {
      if (this.step >= 0 && this.step <= this.text.length) {
        this.step += 1;
      }
    },
    startTest() {
      this.timer = setInterval(() => {
        this.time += 1;
        this.speed = ((this.step / this.time) * 60).toFixed();
        this.accuracityKey(this.uncorrectCount);
      }, 1000);
      this.testStarted = true;
    },
    isExeptionKey(key) {
      if (this.isExeption.find((k) => k === key) === undefined) {
        return false;
      }
      return true;
    },
    accuracityKey(value) {
      this.accuracity = (100 - (value / this.text.length) * 100).toFixed();
    },
  },
  mounted() {
    this.fetchText();
    document.addEventListener('keydown', (e) => {
      this.handlePress(e);
    });
  },
};
</script>

<style scoped>
.main {
  position: relative;
}
</style>
