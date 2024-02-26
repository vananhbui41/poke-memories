<script setup>
import CardFlip from "./Card.vue";
defineProps({
  cardsContext: {
    type: Array,
    default: [],
  },
});
</script>
<template>
  <div class="sceen">
    <h1>Interact Here</h1>
    <card-flip
      v-for="(card, index) in cardsContext"
      :key="index"
      :imgBackFaceUrl="`src/assets/images/${card}.png`"
    />
  </div>
</template>
