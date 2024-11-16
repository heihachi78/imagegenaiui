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
      @input="$emit('update:modelValue', localValue)"
    />
    <input
      type="number"
      v-model.number="localValue"
      :min="min"
      :max="max"
      :step="step"
      @input="$emit('update:modelValue', localValue)"
      class="number-input"
    />
  </div>
</template>

<script lang="ts">
export default {
  props: {
    modelValue: Number,
    label: String,
    min: Number,
    max: Number,
    step: Number,
  },
  data() {
    return {
      id: Math.random().toString(36).substr(2, 9),
      localValue: this.modelValue || 0,
    }
  },
  watch: {
    modelValue(newValue) {
      this.localValue = newValue
    },
  },
}
</script>

<style scoped>
.slider-container {
  margin-top: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}
label {
  font-size: 14px;
  margin-bottom: 5px;
  color: #333;
}
input[type='range'] {
  width: 80%;
  padding: 0;
  appearance: none;
  background-color: #e0e0e0;
  border-radius: 10px;
  height: 6px;
}
input[type='range']::-webkit-slider-thumb {
  -webkit-appearance: none;
  appearance: none;
  width: 10px;
  height: 10px;
  background-color: #007bff;
  cursor: pointer;
  border-radius: 50%;
}
input[type='range']::-moz-range-thumb {
  width: 10px;
  height: 10px;
  background-color: #007bff;
  cursor: pointer;
  border-radius: 50%;
}
.current-value {
  font-size: 12px;
  margin-top: 5px;
  color: #666;
  text-align: center;
  width: 80%;
}
.number-input {
  margin-top: 5px;
  width: 80%;
  text-align: center;
  font-size: 12px;
  color: #666;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 5px;
}
</style>
