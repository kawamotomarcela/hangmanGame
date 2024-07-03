<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router'; 
import './assets/scss/global.scss';
import Form from './components/Form.vue';
import game from './components/Game.vue';

const screen = ref('inicio');
const stage = ref('word');
const word = ref('');
const tip = ref('');
const errors = ref(0);
const letters = ref([]);
const router = useRouter();

function goToAboutPage() {
  router.push('/about'); 
}

function nextStageEtapa(value) {
  if (stage.value === 'word') {
    word.value = value;
    stage.value = 'tip';
  } else if (stage.value === 'tip') {
    tip.value = value;
    screen.value = 'game';
  }
}

function checkLyricstra(letter) {
  return letters.value.find(item => item.toLowerCase() === letter.toLowerCase());
}

function play(letter) {
  letters.value.push(letter);
  checkErrors(letter);
}

function checkErrors(letter) {
  if (word.value.toLowerCase().indexOf(letter.toLowerCase()) >= 0) {
    return checkAccuracies();
  }
  errors.value++;

  if (errors.value === 6) {
    stage.value = 'hanged';
  }
}

function checkAccuracies() {
  let lettersUnicas = [...new Set(word.value.split(''))];
  if (lettersUnicas.length === (letters.value.length - errors.value)) {
    stage.value = 'winner';
  } 
}

function playAgain() {
  word.value = '';
  tip.value = '';
  errors.value = 0;
  letters.value = [];
  screen.value = 'inicio';
  stage.value = 'word';
}

</script>

<template>
  <div id="main">
    <h1>Jogo da Forca  :D</h1>

    <button class="about-button" @click="goToAboutPage">About</button>

    <section v-if="screen === 'inicio'" id="inicio">
      <Form 
        v-if="stage === 'word'"
        title="Defina a Palavra"
        button="Próximo"
        :maxLength="20"
        @nextStage="nextStageEtapa"
      />

      <Form 
        v-if="stage === 'tip'"
        title="Defina a Dica"
        button="Iniciar game"
        :maxLength="40"
        @nextStage="nextStageEtapa"
      />
    </section>

    <section v-else-if="screen === 'game'" id="game">
      <game 
      :errors="errors" 
      :word="word"
      :tip="tip"
      :checkLyricstra="checkLyricstra"
      :stage="stage"
      :letters="letters"
      :play="play"
      :playAgain="playAgain"
      />
    </section>
  </div>
</template>

<style scoped>
#main {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.about-button {
  position: absolute;
  top: 10px;
  right: 10px;
}
</style>
