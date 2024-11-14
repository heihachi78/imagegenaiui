<template>
    <div id="app">
      <div class="container">
        <PromptInput v-model="prompt" />
        <SliderComponent v-model="seedNumber" label="Seed Number" min="1" max="9999" step="1" />
        <SliderComponent v-model="inferenceNumber" label="Inference Number" min="1" max="100" step="1" />
        <SliderComponent v-model="guidanceValue" label="Guidance Value" min="0.1" max="25" step="0.1" />
        <button @click="generateImage">Generate Image</button>
        <ImageDisplay :imageUrl="imageSrc" />
      </div>
    </div>
  </template>
  
  <script>
  import PromptInput from './components/PromptInput.vue';
  import SliderComponent from './components/SliderComponent.vue';
  import ImageDisplay from './components/ImageDisplay.vue';
  
  export default {
    name: 'App',
    components: {
      PromptInput,
      SliderComponent,
      ImageDisplay
    },
    data() {
      return {
        prompt: '',
        inferenceNumber: 50,
        guidanceValue: 7.5,
        seedNumber: 1,
        imageSrc: null
      };
    },
    methods: {
      async generateImage() {
        console.log('Generating image with:', {
          prompt: this.prompt,
          inference_number: this.inferenceNumber,
          guidance_value: this.guidanceValue,
          seed_number: this.seedNumber
        });
  
        try {
          const response = await fetch('http://127.0.0.1:5000/api', {
            method: 'POST',
            headers: {
              'Content-Type': 'application/json'
            },
            body: JSON.stringify({
              prompt: this.prompt,
              infnum: this.inferenceNumber,
              guidance: this.guidanceValue,
              seed: this.seedNumber
            })
          });
  
          if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
          }
  
          // Read the response as an array buffer
          const blob = await response.blob();
  
          // Check if the blob is valid
          if (blob.size === 0 || !blob.type.startsWith('image/')) {
            throw new Error('Invalid image blob');
          }
  
          // Create a data URL from the blob
          this.imageSrc = URL.createObjectURL(blob);
  
          console.log('Created data URL:', this.imageSrc);
        } catch (error) {
          console.error('Failed to fetch image:', error);
        }
      }
    }
  };
  </script>
  
  <style>
  /* Add your styles here */
  #app {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    width: 100vw;
    margin: 0;
    border: 0px solid red; /* Debug line */
  }
  
  .container {
    display: flex;
    flex-direction: column; /* Stack child elements vertically */
    justify-content: center;
    align-items: center;
    width: 80%; /* Example width, adjust as needed */
    box-sizing: border-box; /* Ensure padding and border are included in the element's total size */
    border: 0px solid blue; /* Debug line */
  }
  
  /* Add specific widths and heights to each component if necessary */
  .PromptInput,
  .SliderComponent,
  .ImageDisplay {
    width: 100%; /* Adjust as needed */
    height: auto;
    border: 0px solid green; /* Debug line */
  }
  </style>