<template>
  <div id="app">
    
    <Speach></Speach>


  </div>
</template>

<script>

import Speach from './views/speach.vue';

export default {
  name: 'app',
  components: {
    Speach: Speach
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
