<template>
  <div class="card" :class="{ disabled: isDisabled }">
    <div
      class="card-inner"
      :class="{ 'is-flipped': isFlipped }"
      @click="onToggleFlipCard()"
    >
      <div class="card-face card-face-front">
        <div class="card-content"></div>
      </div>
      <div class="card-face card-face-back">
        <div
          class="card-content"
          :style="{
            backgroundImage: `url(${props.imgBackFaceUrl})`,
          }"
        ></div>
      </div>
    </div>
  </div>
</template>
<script setup>
import { ref, defineExpose } from "vue";
const props = defineProps({
  card: {
    type: [Number, Object]
  },
  imgBackFaceUrl: {
    type: String,
    required: true,
  },
})
const isFlipped = ref(false);
const isDisabled = ref(false);

const emit = defineEmits(['onFlip'])
const onToggleFlipCard = () => {
  if (isDisabled.value) return false;
  isFlipped.value = !isFlipped.value;
  if (isFlipped.value) {
    emit("onFlip", props.card);
  }
};
const onFlipBackCard = () => {
  isFlipped.value = false;
};
const onDisableClick = () => {
  isDisabled.value = true;
};

defineExpose({
  onFlipBackCard,
  onDisableClick
}); 
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
.card-face-front .card-content {
  background: url("../assets/images/icon_back.png") no-repeat center center;
  background-size: 40%;
  height: 100%;
  width: 100%;
}
.card-face-back {
  background-color: var(--light);
  transform: rotateY(-180deg);
}
.card-face-back .card-content {
  background-size: contain;
  background-position: center center;
  background-repeat: no-repeat;
  height: 100%;
  width: 100%;
}

.card.disabled .card-innner{
  cursor: false;
}
</style>
