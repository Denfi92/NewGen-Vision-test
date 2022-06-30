<template>
  <main class="main container">
    <h2 class="center-align">Начинайте печатать</h2>
    <div class="center-align">
      <span
        v-for="(letter, idx) in text"
        :key="idx"
        :class="[(hasTyping && letter == textArr[idx]) ? 'correct' : '',
        (hasTyping && (idx == textArr.length) && !isCorrect) ? 'error' : '']"
      >{{letter}}</span>
    </div>
    <label for="textarea">
      <textarea name="textarea" class="textarea" ref="typing-textarea" @keydown="keyWatch">
      </textarea>
    </label>
    <div class="main-menu">
      <button class="btn btn-start" @click="startTyping">Начать</button>
      <button class="btn btn-again">Заново</button>
    </div>
    <div class="main-result">
      <span class="main-result__degree">%</span>
      <span class="main-result__symbols">знаки в минуту</span>
    </div>
    <div class="main-stats">
      <h3 class="main-stats__title">Результат</h3>
      <div class="main-stats__result">
        <span class="main-stats__speed">Ваша скорость:</span>
        <span class="main-stats__accuracity">Ваша точность:</span>
        <span></span>
      </div>
    </div>
  </main>
</template>

<script>
export default {
  name: 'TypingArea',
  data() {
    return {
      text: '',
      textArr: [],
      symbols: 0,
      timer: null,
      minutes: 0,
      error: false,
      hasTyping: false,
      isFinished: false,
    };
  },
  methods: {
    async fetchText() {
      const response = await fetch('https://baconipsum.com/api/?type=all-meat&sentences=1&start-with-lorem=1');
      const res = await response.json();
      this.text = res.join();
    },
    startTyping() {
      // this.timer = setInterval(() => {
      //   this.minutes += (1 / 60);
      // }, 1000);
      console.log(this.hasTyping);
      this.hasTyping = true;
      console.log(this.hasTyping);
      // console.log(this.timer);
      // console.log(this.minutes);
    },
    keyWatch(e) {
      this.textArr.push(e.key);
      console.log(this.textArr);
    },
    handleType() {
      this.textArr.pop();
      this.symbols += +1;
    },
  },
  computed: {
    textArrNew() {
      return this.text.split('');
    },
    isCorrect() {
      const i = this.textArr.length;
      if (this.textArr[i - 1] !== this.textArrNew[i - 1]) {
        this.handleType();
        return false;
      }
      return true;
    },
  },
  mounted() {
    this.$refs['typing-textarea'].focus();
    this.fetchText();
  },
};

</script>

<style scoped>
  .main-subtitle {
    text-align: center;
  }

  .correct {
    color: green;
  }

  .error {
    color: red;
  }
</style>
