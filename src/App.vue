<template>
  <div id="app">
    <img src="./assets/logo.png">
    <hello></hello>
    <div class="row">
      <div class="small-2 large-4 columns"><!-- ... --></div>
      <div class="small-4 large-4 columns"><!-- ... --></div>
      <div class="small-6 large-4 columns"><!-- ... --></div>
    </div>
  </div>
</template>

<script>
import Hello from './components/Hello';

export default {
  name: 'app',
  components: {
    Hello,
  },
};
</script>

<style lang="scss">
@import '~foundation-sites/scss/foundation';
@include foundation-everything;

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
