<template>
  <div class="game" v-on:click.exact="clickOnInterface">
    <span class="round" ref="round" v-on:click.exact.stop="clickOnRound" v-on:click.alt.stop="bonus"></span>
  </div>
</template>

<script>
export default {
  name: 'game',
  data: function () {
    return {
      click: 0
    }
  },
  created: function () {
    document.onkeydown = this.start
  },
  // ici c'est watch car on ne regarde pas une propriété, donc ce n'est pas updated
  watch: {
    click: function () {
      this.updateRound()
    }
  },
  methods: {
    clickOnRound: function (event) {
      this.click++
    },
    bonus: function (event) {
      console.log('BONUS')
    },
    clickOnInterface: function () {
      this.click++
    },
    start: function (event) {
      if (event.key === 'Enter') {
        console.log('START')
      }
    },
    updateRound: function () {
      let element = this.$refs.round

      let size = Math.random() * (100 - 10) + 10
      let top = Math.random() * (60 - 5) + 5
      let left = Math.random() * (60 - 5) + 5

      element.style.width = element.style.height = `${size}px`
      element.style.margin = `${top}% ${left}%`
    }
  }
}
</script>

<style scoped>
    .game {
        width: 100%;
        height: 50%;
        display: block;
        background: darkslategrey
    }
    .round {
        width: 50px;
        height: 50px;
        background: cornsilk;
        border-radius: 9999px;
        position: absolute;
        margin: 20% 20%
    }
</style>
