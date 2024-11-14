<template>
    <div v-if="imageUrl">
      <img :src="imageUrl" alt="Generated Image" />
    </div>
    <div v-else>
      No image generated yet.
    </div>
  </template>
  
  <script>
  export default {
    props: {
      imageUrl: String
    }
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  img {
    max-width: 100%;
    border-radius: 8px;
  }
  div {
    margin-top: 20px;
    text-align: center;
  }
  </style>