<template>
  <div>
    <label for="text">
      <input type="text" v-model="text">
    </label>
  </div>
</template>

<script>
export default {
  name: 'TypingArea',
  data() {
    return {
      text: '',
    };
  },
  methods: {
    async fetchText() {
      const response = await fetch('https://baconipsum.com/api/?type=all-meat&sentences=1&start-with-lorem=1');
      const res = await response.json();
      this.text = res;
      console.log(res);
    },
  },
  mounted() {
    this.fetchText();
  },
};

</script>
