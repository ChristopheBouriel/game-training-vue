<template>
  <div class="game">
    <span class="round"></span>
  </div>
</template>

<script>
export default {
  name: 'game'
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
