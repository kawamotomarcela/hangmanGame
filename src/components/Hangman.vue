<script>
export default {
  name: 'Forca',
  props: {
    errors: {
      type: Number,
      required: true
    }
  },
  data() {
    return {};
  },
  methods: {}
}
</script>

<template>
  <div class="forca">
    <img :src="`https://raw.githubusercontent.com/william-costa/wdev-hangman-game-resources/master/images/hangman/${errors}.svg`" />
  </div>
</template>


<style lang="scss">

@import '../assets/scss/global.scss';

.forca img{
    height: 150px;
}
</style>