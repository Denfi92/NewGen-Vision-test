<template>
  <div class="main-result row">
    <h3 class="main-result__title">Ваш результат:</h3>
    <div class="main-result__result">
      <div class="main-result__speed">скорость: {{ speed }} зн/мин</div>
      <div class="main-result__accuracity">точность:  {{ accuracity }}%</div>
      <span></span>
    </div>
  </div>
</template>
<script>
export default {
  props: ['speed', 'accuracity'],
};

</script>

<style scoped>
  .main-result {
    padding: 20px;
    font-weight: bold;
  }
</style>
