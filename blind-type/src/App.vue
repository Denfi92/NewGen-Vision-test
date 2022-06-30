<template>
  <h1 class="center-align">Тренажер слепой печати</h1>
  <TypingArea />
</template>

<script>
import TypingArea from './components/TypingArea.vue';

export default {
  name: 'App',
  components: {
    TypingArea,
  },
};
</script>

<style lang="scss">
@import '~materialize-css/dist/css/materialize.min.css';

body {
  max-width: 1200px;
  margin: 0 auto;
}

</style>
