<script setup>
import CardFlip from "./Card.vue";
import { ref, onMounted } from "vue";

const props = defineProps({
  cardsContext: {
    type: Array,
    default: [],
  },
});
const emit = defineEmits(["onFinished"]);
const rules = ref([]);
const cardRefs = ref([]);
const disabledCardsCount = ref(0);
const setCardRef = (el, index) => {
  cardRefs.value[index] = el;
};
onMounted(() => {
  // Initialize cardRefs array with null values
  cardRefs.value = Array(props.cardsContext.length).fill(null);
});
const checkRules = (card) => {
  if (rules.value.length == 2) return false;

  rules.value.push(card);
  if (rules.value.length == 2 && rules.value[0].value == rules.value[1].value) {
    cardRefs.value[rules.value[0].index].onDisableClick();
    cardRefs.value[rules.value[1].index].onDisableClick();

    rules.value = [];

    // Check the count of disabled cards here
    disabledCardsCount.value += 2;
    if (disabledCardsCount.value === props.cardsContext.length) {
      // All cards are disabled, emit event or execute further logic
      setTimeout(() => {
        emit("onFinished");
      }, 900);
    }
  } else if (
    rules.value.length == 2 &&
    rules.value[0].value != rules.value[1].value
  ) {
    console.log("False...");
    setTimeout(() => {
      console.log(cardRefs.value[rules.value[0].index]);
      // Flip back the cards after a delay
      cardRefs.value[rules.value[0].index].onFlipBackCard();
      cardRefs.value[rules.value[1].index].onFlipBackCard();
      rules.value = [];
    }, 800);
  } else return false;
};
</script>
<template>
  <div class="sceen">
    <h1>Interact Here</h1>
    <card-flip
      v-for="(card, index) in props.cardsContext"
      :key="index"
      :ref="(el) => setCardRef(el, index)"
      :imgBackFaceUrl="`src/assets/images/${card}.png`"
      :card="{ index, value: card }"
      @onFlip="checkRules($event)"
    />
  </div>
</template>
