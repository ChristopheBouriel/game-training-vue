<template>
  <div class="content">
    <div class="game" @click.exact="clickOnInterface" :class="{wait: !player}">
      <span v-if="player" class="round" :style="roundStyle" :class="{bonus: bonusActivated, badColor: badColorActivated}" @click.exact.stop="clickOnRound" @click.alt.stop="bonus"></span>
    </div>
    <div class="log">
      <p v-for="(item, index) in infoUser" :key=index>
        #{{item.id / 2}} - {{item.message}}
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'game',
  props: ['player'],
  data: function () {
    return {
      click: 0,
      roundStyle: {
        height: '50px',
        width: '50px',
        margin: '20% 20%'
      },
      bonusActivated: false,
      badColorActivated: false,
      collection: []
    }
  },
  computed: {
    infoUser: function () {
      return this.collection.filter(item => item.type === 'user')
    }
  },
  created: function () {
    document.onkeydown = this.start
  },
  // ici c'est watch car on ne regarde pas une propriété, donc ce n'est pas updated
  watch: {
    click: function () {
      this.updateRound()
      this.$emit('score', this.click)
    }
  },
  methods: {
    clickOnRound: function (event) {
      setTimeout(this.updateRound, 1000)
      this.updateClick(1)
      this.addLog(`Bravo !`)
    },
    bonus: function (event) {
      if (this.bonusActivated) {
        this.updateClick(2)
        this.addLog(`Perfect ! + 2`)
      } else {
        this.updateClick()
        this.addLog(`What !? - 1`)
      }
    },
    clickOnInterface: function () {
      this.updateClick()
      this.addLog(`Ho no ! - 1`)
    },
    updateClick: function (increment) {
      if (!this.player) {
        return
      }
      if (increment) {
        this.click += increment
      } else {
        this.click--
      }
    },
    start: function (event) {
      if (event.key === 'Enter') {
        console.log('START')
      }
    },
    updateRound: function () {
      let size = Math.random() * (100 - 10) + 10
      let top = Math.random() * (30 - 2) + 2
      let left = Math.random() * (80 - 2) + 2

      this.bonusActivated = size > 80
      this.badColorActivated = size < 20

      this.addLog({
        size: size,
        top: top,
        left: left
      }, 'round')

      this.roundStyle.width = this.roundStyle.height = `${size}px`
      this.roundStyle.margin = `${top}% ${left}%`
    },
    addLog: function (message, type) {
      if (!this.player) {
        return
      }
      let typeOfMessage = type || 'user'
      this.collection.unshift({id: this.collection.length, message: message, type: typeOfMessage})
    }
  }
}
</script>

<style scoped>
    .content {
      height: 400px;
    }
    .log {
      width: 100%;
      height: 35px;
      background: rgb(22, 38, 38);
      display: block;
      text-align: center;
      overflow: hidden;
      padding: 6px;
      color: whitesmoke;
    }
    .game {
      width: 100%;
      height: 85%;
      display: block;
      background: darkslategrey;
      opacity: 1;
      transition: opacity 1s;
    }
    .round {
      background: cornsilk;
      border-radius: 9999px;
      position: absolute;
      transition: width 2s, height 2s, margin 0.5s;
    }
    .bonus {
      background: rgb(255, 170, 0);
    }
    .badColor {
      background: rgb(47, 84, 84)
    }
    .wait {
      opacity: 0.3
    }
</style>
