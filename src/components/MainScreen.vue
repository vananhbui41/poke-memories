<template>
  <div class="main">
    <h1>POKE MEMORIES</h1>
    <h3>Select node to start game</h3>
    <div class="actions">
      <button @click="startGame(16)">
        <span>4x4</span>
        <span>Easy</span>
      </button>
      <button @click="startGame(36)">
        <span>6x6</span>
        <span>Normal</span>
      </button>
      <button @click="startGame(64)">
        <span>8x8</span>
        <span>Hard</span>
      </button>
      <button @click="startGame(100)">
        <span>10x10</span>
        <span>Super Hard</span>
      </button>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['startGame'])
const startGame = (totalOfBlocks) => {
  emit("startGame", { totalOfBlocks });
};
</script>
