<template>
   <button class="button">{{ text }}</button>
</template>

<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'HelloWorld',
  props: {
    text: String,
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
  .button {
    cursor: pointer;
    display: inline-block;
    padding: 0.7vw;
    background: tomato;
    font-size: 0.7vw;
    color: #fff;
    border: 0;

    &:hover,
    &:focus {
        background: darken(tomato, 20%);
    }
  }
</style>