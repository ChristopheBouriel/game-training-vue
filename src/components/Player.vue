<template>
  <div>
      <span v-html="welcomeMessage" v-hide></span>
      <form v-hide>
            <input name="player" placeholder="Entrez votre nom" v-border:blue>
            <button type="submit">
                Jouer
            </button>
      </form>
  </div>
</template>

<script>
export default {
  name: 'player',
  created: function () {
      this.player = 'Tof'
      this.playerClass = this.player ? 'player' : 'playerForm'
      this.welcomeMessage = this.player ? `Bonjour <span class="player"> ${this.player} </span> !` : ''
  },
  directives: {
      border: function (el, binding) {
          el.style.borderColor = binding.arg
      },
      hide: function (el, binding, vnode) {
          let isForm = vnode.tag === 'form'
          let player = vnode.context.player
          if (isForm) {
              el.style.display = player ? 'none' : 'block'
          } else {
              el.style.display = player ? 'block' : 'none'
          }
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