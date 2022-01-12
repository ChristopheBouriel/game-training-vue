<template>
  <div id="app">
    <game :player="player" v-on:score="updateScore"></game>
    <player v-on:player="updatePlayer"></player>
    <score :score="score" :player="player"></score>
    <!--<router-view/>-->
  </div>
</template>

<script>
import Game from './components/Game'
import Player from './components/Player'
import Score from './components/Score'

export default {
  name: 'App',
  data: function () {
    return {
      score: 0,
      player: false
    }
  },
  components: {
    Game,
    Score,
    Player
  },
  methods: {
    updateScore: function (score) {
      this.score = score
    },
    updatePlayer: function () {
      this.player = true
    }
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
