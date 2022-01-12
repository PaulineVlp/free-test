<template>
  <div id="app">
    <img alt="logo" width="20%" src="./assets/movie-logo.png">
    <h1>Clap, bonjour!</h1>
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

@import url('https://fonts.googleapis.com/css2?family=Oswald:wght@700&display=swap');

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1{
  color: white;
  text-align: center;
  font-weight: bold;
  font-family: 'Oswald';
  margin-bottom: 30px;
}
body {
  background-image: url('https://image.freepik.com/photos-gratuite/fond-bleu-degrade-luxe-abstrait-bleu-fonce-lisse-banniere-studio-vignette-noire_1258-52535.jpg');
  background-size: cover;
}
</style>
