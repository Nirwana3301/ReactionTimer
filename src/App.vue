<template>
  <div class="main">
    <div class="wrapper">
      <h1>Reaction TImer</h1>
      <button :disabled="isPlaying" @click="start()">Start</button>
      <span v-if="isPlaying">Scroll down!</span>
      <Results v-if="showResults" :score="score" />
    </div>
    <div class="block-wrapper">
      <Block v-if="isPlaying" :delay="delay" @end="endGame" />
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Block from "./components/Block.vue";
import Results from "./components/Results.vue";

let isPlaying = ref(false);
let delay = ref(null);
let score = ref(null);
let showResults = ref(false);

const start = () => {
  delay.value = 2000 + Math.random() * 5000;
  isPlaying.value = true;
  showResults.value = false;
};

const endGame = (reactionTime) => {
  score.value = reactionTime;
  isPlaying.value = false;
  showResults.value = true;
};
</script>

<style>
.main {
  height: 100vh;
  width: 100vw;
}

.wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #000;
  color: #fff;
}

.wrapper > * {
  margin: 1rem;
}

.block-wrapper {
  height: 60rem;
  width: 100%;
}

span {
  font-size: 2rem;
  font-weight: bold;
  color: tomato;
}
</style>
