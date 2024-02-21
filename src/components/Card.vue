<template>
  <div class="card">
    <div
      class="card-inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard()"
    >
      <div class="card-face card-face-front">
        <div class="card-content">Front</div>
      </div>
      <div class="card-face card-face-back">
        <div class="card-content">Back</div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref } from "vue";
const isFlipped = ref(false);

const onToggleFlipCard = () => {
  isFlipped.value = !isFlipped.value;
};
</script>
<style scoped>
.card {
  display: inline-block;
  margin-right: 1rem;
  margin-bottom: 1rem;
  width: 90px;
  height: 120px;
}
.card-inner {
  width: 100%;
  height: 100%;
  transition: transform 0.5s;
  transform-style: preserve-3d;
  cursor: pointer;
  position: relative;
}
.card-inner.is-flipped {
  transform: rotateY(-180deg);
}
.card-face {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  overflow: hidden;
  border-radius: 1rem;
  padding: 1rem;
  box-shadow: 0 3px 10px 3px rgba(0, 0, 0, 0.2);
}
.card-face-back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
</style>
