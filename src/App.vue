<script setup>
import "./assets/styles/global.css";
import { ref, reactive } from "vue";
import MainScreen from "./components/MainScreen.vue";
import InteractScreen from "./components/InteractScreen.vue";

const statusMatch = ref("default");
const settings = reactive({
  totalOfBlocks: 0,
  cardsContext: [],
});

const onHandleBeforeStart = (config) => {
  console.log("running before start", config);
  settings.totalOfBlocks = config.totalOfBlocks;
  const firstCards = Array.from(
    { length: settings.totalOfBlocks / 2 },
    (_, i) => i + 1
  );
  console.log(firstCards);
  statusMatch.value = "match";
};
</script>

<template>
  <main-screen
    v-if="statusMatch === 'default'"
    @startGame="onHandleBeforeStart($event)"
  />
  <interact-screen v-if="statusMatch === 'match'" />
</template>
