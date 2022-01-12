<template>
    <div class="row">
        <div class="score mx-auto" v-if="player">
            {{ score }}
        </div>
    </div>
</template>

<script>
export default {
  name: 'score',
  props: ['score', 'player']
}
</script>

<style scoped>
    .score {
        display: inline-block;
        text-align: center;
        height: 50px;
        width: 150px;
        font-size: 1.5em;
        color: greenyellow;
        background: rgb(46, 46, 46);
        padding: 10px;
        border-radius: 4px;
    }
</style>
