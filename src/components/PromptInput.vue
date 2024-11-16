<template>
  <label :for="id">{{ label }}</label>
  <textarea
    v-model="localValue"
    @input="$emit('update:modelValue', localValue)"
    placeholder="Enter prompt"
  ></textarea>
</template>

<script lang="ts">
export default {
  props: {
    modelValue: String,
    label: String,
  },
  data() {
    return {
      localValue: this.modelValue || '',
    }
  },
}
</script>

<style scoped>
textarea {
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  min-height: 80px;
  resize: vertical;
  width: 80%;
  box-sizing: border-box;
  font-family: 'Arial', sans-serif;
}
label {
  font-size: 14px;
  margin-bottom: 5px;
  color: #333;
}
</style>
