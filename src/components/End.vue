<script>
export default {
  name: 'Final',
  props: {
    stage: {
      type: String,
      required: true
    },
    text: {
      type: String,
      required: true
    },
    playAgain: {
      type: Function,
      required: true
    }
  }
}
</script>

<template>
 <div class="final">
  <div :class="`final-text ${stage}`">
  {{ text }}
  </div>
  <button class="final-botão" @click="playAgain">Jogar Novamente</button>
 </div>
</template>

<style lang="scss">
@import '../assets/scss/global.scss';

.final-text{
  margin:20px 0px;
  font-size:24px;
  font-weight: bold;
}
.final-text.hanged{
  color: $red;
}
.final-text.winner{
  color: $green;
}
</style>
