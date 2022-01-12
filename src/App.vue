<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Recherche/>
  </div>
</template>

<script>
import Recherche from './components/Recherche.vue'

export default {
  name: 'App',
  components: {
    Recherche
  }
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
