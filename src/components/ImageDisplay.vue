<template>
  <div v-if="isLoading">Generating image, please wait...</div>
  <div v-else-if="hasError">Something went wrong. Please try again.</div>
  <div v-else-if="imageUrl">
    <img :src="imageUrl" alt="Generated Image" />
  </div>
  <div v-else>No image generated yet.</div>
</template>

<script lang="ts">
export default {
  props: {
    imageUrl: String,
    isLoading: Boolean, // Add loading state prop
    hasError: Boolean, // Add error state prop
  },
}
</script>

<style scoped>
/* Add your styles here */
img {
  max-width: 100%;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}
div {
  margin-top: 20px;
  text-align: center;
  color: #666;
  font-family: 'Arial', sans-serif;
}
</style>
