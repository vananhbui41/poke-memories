<script setup>
import "./assets/styles/global.css";
import { ref, reactive } from "vue";
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";
import ResultScreen from "./components/ResultScreen.vue";
import { shuffled } from "./utils/array";

const statusMatch = ref("default");
const timer = ref(0);
const settings = reactive({
  totalOfBlocks: 0,
  cardsContext: [],
  startAt: null,
});

const onHandleBeforeStart = (config) => {
  settings.totalOfBlocks = config.totalOfBlocks;
  const firstCards = Array.from(
    { length: settings.totalOfBlocks / 2 },
    (_, i) => i + 1
  );

  const secondCards = [...firstCards];
  const cards = [...firstCards, ...secondCards];
  settings.cardsContext = shuffled(shuffled(shuffled(shuffled(cards))));
  settings.startAt = new Date().getTime();

  statusMatch.value = "match";
};
const onShowResult = () => {
  // get time
  timer.value = new Date().getTime() - settings.startAt;
  
  // switch to Result Componet
  statusMatch.value = "result";
}
</script>

<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @startGame="onHandleBeforeStart($event)"
  />
  <interact-screen
    v-if="statusMatch === 'match'"
    :cardsContext="settings.cardsContext"
    @onFinished="onShowResult()"
  />
  <result-screen 
    v-if="statusMatch === 'result'"
    :timer="timer"
    @onStartAgain="statusMatch = 'default'"
  />
</template>
