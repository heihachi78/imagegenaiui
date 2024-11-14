<template>
    <div class="slider-container">
      <label :for="id">{{ label }}</label>
      <input 
        type="range" 
        :id="id" 
        v-model="localValue" 
        :min="min" 
        :max="max" 
        :step="step" 
        @input="$emit('update:modelValue', localValue)" />
      <div class="current-value">{{ localValue }}</div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      modelValue: Number,
      label: String,
      min: Number,
      max: Number,
      step: Number
    },
    data() {
      return {
        id: Math.random().toString(36).substr(2, 9),
        localValue: this.modelValue || 0
      };
    }
  };
  </script>
  
  <style scoped>
  /* Add your styles here */
  .slider-container {
    margin-top: 10px;
  }
  label {
    font-size: 16px;
    margin-bottom: 5px;
  }
  input[type="range"] {
    width: 100%;
    padding: 0;
    appearance: none;
    background-color: #f3f3f3;
    border-radius: 20px;
  }
  input[type="range"]::-webkit-slider-thumb {
    -webkit-appearance: none;
    appearance: none;
    width: 36px;
    height: 36px;
    background-color: #4CAF50;
    cursor: pointer;
    border-radius: 50%;
  }
  input[type="range"]::-moz-range-thumb {
    width: 36px;
    height: 36px;
    background-color: #4CAF50;
    cursor: pointer;
    border-radius: 50%;
  }
  .current-value {
    font-size: 14px;
    margin-top: 5px;
  }
  </style>