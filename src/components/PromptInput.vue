<template>
    <textarea v-model="localValue" @input="$emit('update:modelValue', localValue)" placeholder="Enter prompt"></textarea>
  </template>
  
  <script>
  export default {
    props: {
      modelValue: String
    },
    data() {
      return {
        localValue: this.modelValue || ''
      };
    }
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  textarea {
    padding: 10px; /* Increased padding for a bigger textarea box */
    font-size: 16px; /* Increased font size for better visibility */
    border: 1px solid #ccc;
    border-radius: 4px;
    min-height: 100px; /* Minimum height to ensure it's not too small */
    resize: vertical, horizontal; /* Allow vertical resizing of the textarea */
  }
  </style>