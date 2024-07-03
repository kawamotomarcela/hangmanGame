<script>
import Forca from './Hangman.vue';
import Word from './Word.vue';
import keyboard from './Keyboard.vue';
import Final from './End.vue';

export default {
  name: "Game",
  components: {
    Forca,
    Word,
    keyboard,
    Final
  },
  props: {
    errors: {
      type: Number,
      required: true
    },
    word: {
      type: String,
      required: true
    },
    tip: {
      type: String,
    },
    checkLyricstra: {
      type: Function,
      required: true
    },
    stage: {
      type: String,
      required: true
    },
    letters: {
      type: Array,
      required: true
    },
    play: {
      type: Function,
      required: true
    },
    playAgain: {
      type: Function,
    }
  }
};
</script>

<template>
  <div class="game">

    <Forca 
    :errors="errors"
     />

    <word
      :word="word"
      :tip="tip"
      :checkLyricstra="checkLyricstra"
      :stage="stage"
    />

    <keyboard
       v-if="stage !== 'hanged' && stage !== 'winner'"
      :letters="letters"
      :checkLyricstra="checkLyricstra"
      :play="play"
    />

    <Final
      v-if="stage === 'hanged' || stage === 'winner'"
      :stage="stage"
      :text="stage === 'winner' ? 'Parabéns, você acertou!' : 'Fim de jogo, tente novamente =('"
      :playAgain="playAgain"
    />

  </div>
</template>

<style lang="scss">
@import "../assets/scss/global.scss";
</style>


