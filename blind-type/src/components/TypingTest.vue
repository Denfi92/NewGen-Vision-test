<template>
  <h1 class="center-align">Тренажер слепой печати</h1>
  <h3 class="center-align subtitle">
    {{testStarted ? `Пройденое время: ${time}` : 'Просто начните печатать'}}
  </h3>
  <div class="center-align row text z-depth-4">
    <span v-for="(letter, idx) in text" :key="idx" class="text">
      <span v-if="idx == step">
        <span class="correct" :class="{uncorrectChar: uncorrectChar}">{{ letter }}</span>
      </span>
      <span v-else>{{letter}}</span>
    </span>
  </div>
</template>

<script>
export default {
  props: ['text', 'step', 'time', 'uncorrectChar', 'testStarted'],
};

</script>

<style scoped>

.correct {
  background-color: green;
  padding: 0px 3px 2px 3px;
  border-radius: 5px;
  font-size: 24px;
}

.uncorrectChar {
  background-color: red !important;
}
.subtitle {
  margin-bottom: 50px;
}

.text {
  padding-top: 30px;
  margin-bottom: 50px;
  height: 100px;
  font-weight: bold;
}
</style>
