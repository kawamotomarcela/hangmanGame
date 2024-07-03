<script>
export default {
  name: 'Keyboard',
  props: {
    letters: {
      type: Array,
      required: true
    },
    checkLyricstra: {
      type: Function,
      required: true
    },
    play: {
      type: Function,
      required: true
    }
  }
}
</script>

<template>
  <div class="keyboard">
    <button class="keyboard-button"
      v-for="(letter, key) in 'abcdefghijklmnopqrstuvwxyz'"
      :key="key"
      :disabled="checkLyricstra(letter)"
      @click="play(letter)">
      {{ letter }}
    </button>
  </div>
</template>

<style lang="scss">
@import '../assets/scss/global.scss';
.keyboard {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;
  width: 60%;
  margin: 40px auto;

  .keyboard-button {
    margin: 5px;
    padding: 10px 20px;
    text-transform: uppercase;
    background-color: #4eb380;
    color: white;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s ease;

    &:hover {
      background-color: #369972;
    }
  }
}

</style>
