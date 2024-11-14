<script setup>
import { ref } from 'vue'
const count = ref(0)
</script>

<template>
    <p>{{ count }}</p>
    <button @click="count--">-</button>
    <button @click="count++">+</button>
</template>

<style scoped>
button {
  font-weight: bold;
}
p {
  font-weight: bold;
}
</style>