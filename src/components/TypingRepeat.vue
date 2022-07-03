<template>
  <div class="main-menu center-align">
    <button
      class="btn waves-effect waves-light"
      @click="$emit('repeatTest')"
      onclick="this.blur()">{{testStarted ? 'Заново' : 'Новый текст'}}</button>
  </div>
</template>

<script>
export default {
  props: ['testStarted'],
  emits: ['repeatTest'],
};

</script>
