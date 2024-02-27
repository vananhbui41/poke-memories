<template>
    <div class="screen">
        <h1>Congraturation</h1>
        <p> {{ Math.round(timer/1000) }} second </p>
        <button >Start Again</button>
    </div>
</template>

<script setup>
    defineProps({
        timer: {
            type: Number,
            required: true
        }
    })
</script>
