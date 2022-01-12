<template>
    <div>
        {{ score ? 'Votre score : ' + score : 'Appuyez sur la touche entrée pour démarrer' }}
    </div>
</template>

<script>
export default {
  name: 'score',
  data: function () {
    return {
      score: 0
    }
  }
}
</script>

<style scoped>

</style>
