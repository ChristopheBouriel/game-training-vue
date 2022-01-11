<template>
  <div id="app">
    <img src="./assets/logo.png">
    <game></game>
    <player></player>
    <score></score>
    <!--<router-view/>-->
  </div>
</template>

<script>
import Game from './components/Game'
import Player from './components/Player'
import Score from './components/Score'

export default {
  name: 'App',
  components: {
    Game,
    Score,
    Player
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 1000px;
  display: block;
}
</style>
