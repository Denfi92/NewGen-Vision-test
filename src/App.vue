<template>
  <typing-area></typing-area>
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
    background-color: lightgrey;
  }
</style>
