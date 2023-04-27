# The Loading Indicator

## The Prompt

**Q**: `I want you to add a loading indicator in place of the button whenever we wait for the response from our API`

**A**: `To add a loading indicator in place of the button while waiting for the response, you can create a new ref isLoading and toggle its value when the request is being made. You can then conditionally render the button or the loading indicator in the template based on the value of isLoading. Here's how you can modify your component:`

```html
<script setup lang="ts">
import { ref } from 'vue';
import { useFetch } from 'nuxt3';

const title = ref('');
const description = ref('');
const image = "https://thumbs.dreamstime.com/b/pizza-rustic-italian-mozzarella-cheese-basil-leaves-35669930.jpg";
const message = ref('');
const isLoading = ref(false);

const submitPost = async (): Promise<void> => {
  console.log('Title:', title.value);
  console.log('Description:', description.value);

  // Set isLoading to true while waiting for the response
  isLoading.value = true;

  try {
    // Fetch the message from the API
    const { data } = await useFetch('/api/chat-completion', {
      method: 'POST',
      body: { description: description.value },
    });
    message.value = data.message;
  } finally {
    // Set isLoading back to false after the response is received
    isLoading.value = false;
  }
};
</script>

<template>
  <!-- Your existing template content -->

  <!-- Form section -->
  <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 w-full md:w-2/3 lg:w-1/2 mx-auto">
    <!-- Existing form content -->

    <div class="flex items-center justify-center">
      <!-- Conditionally render the button or the loading indicator -->
      <button
        v-if="!isLoading"
        class="bg-accent hover:bg-accent-light text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        type="submit"
        @click="submitPost"
      >
        Submit
      </button>
      <div v-else class="loader w-6 h-6 text-accent"></div>
    </div>
  </div>

  <!-- Social Media Card section -->
  <!-- Your existing social media card content -->
</template>

<style scoped>
.bg-accent {
  background-color: #41b883;
}
.bg-accent-light {
  background-color: #63d5a3;
}
.loader {
  border: 2px solid #f3f3f3;
  border-top: 2px solid #41b883;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
```
