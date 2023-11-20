<template>
  <switcher />
</template>

<script>

import switcher from './components/switcher.vue';

export default {
  name: 'App',
  components: { switcher }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
