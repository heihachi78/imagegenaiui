<template>
  <div id="app">
    <div class="container">
      <div class="controls">
        <PromptInput v-model="positivePrompt" label="Positive prompt" />
        <PromptInput v-model="negativePrompt" label="Negative prompt" />
        <SliderComponent
          v-model="seedNumber"
          label="Seed number"
          min="1"
          max="9999999999"
          step="1"
        />
        <SliderComponent
          v-model="inferenceNumber"
          label="Inference number"
          min="1"
          max="100"
          step="1"
        />
        <SliderComponent
          v-model="guidanceValue"
          label="Guidance value"
          min="0.1"
          max="25"
          step="0.1"
        />
        <button @click="generateImage">Generate Image</button>
      </div>
      <div class="image-display">
        <ImageDisplay :imageUrl="imageSrc" :isLoading="isLoading" :hasError="hasError" />
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import PromptInput from './components/PromptInput.vue'
import SliderComponent from './components/SliderComponent.vue'
import ImageDisplay from './components/ImageDisplay.vue'

export default {
  name: 'App',
  components: {
    PromptInput,
    SliderComponent,
    ImageDisplay,
  },
  data() {
    return {
      positivePrompt: '',
      negativePrompt: '',
      inferenceNumber: 50,
      guidanceValue: 7.5,
      seedNumber: 1,
      imageSrc: null,
      isLoading: false, // Add loading state
      hasError: false, // Add error state
    }
  },
  methods: {
    async generateImage() {
      this.isLoading = true // Set loading state to true
      this.hasError = false // Reset error state
      this.imageSrc = null // Clear previous image

      console.log('Generating image with:', {
        positive_prompt: this.positivePrompt,
        negative_prompt: this.negativePrompt,
        inference_number: Number(this.inferenceNumber),
        guidance_value: Number(this.guidanceValue),
        seed_number: Number(this.seedNumber),
      })

      try {
        const response = await fetch('http://127.0.0.1:5000/generate', {
          method: 'POST',
          headers: {
            'Content-Type': 'application/json',
          },
          body: JSON.stringify({
            positive_prompt: this.positivePrompt,
            negative_prompt: this.negativePrompt,
            infnum: Number(this.inferenceNumber),
            guidance: Number(this.guidanceValue),
            seed: Number(this.seedNumber),
          }),
        })

        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`)
        }

        // Read the response as an array buffer
        const blob = await response.blob()

        // Check if the blob is valid
        if (blob.size === 0 || !blob.type.startsWith('image/')) {
          throw new Error('Invalid image blob')
        }

        // Create a data URL from the blob
        this.imageSrc = URL.createObjectURL(blob)

        console.log('Created data URL:', this.imageSrc)
      } catch (error) {
        console.error('Failed to fetch image:', error)
        this.hasError = true // Set error state to true
      } finally {
        this.isLoading = false // Set loading state to false
      }
    },
  },
}
</script>

<style>
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
  margin: 0;
  background-color: #f5f5f5;
  font-family: 'Arial', sans-serif;
}

.container {
  display: flex;
  width: 80%;
  box-sizing: border-box;
  background: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.controls {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-right: 20px;
}

h3 {
  margin: 10px 0 5px;
  font-size: 16px;
  color: #333;
}

button {
  padding: 10px 20px;
  font-size: 14px;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 10px;
  width: 80%;
}

button:hover {
  background-color: #0056b3;
}

.image-display {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #e0e0e0;
  border-radius: 8px;
}
</style>
