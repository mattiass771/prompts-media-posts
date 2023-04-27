# Connect The Puzzle

## The Prompt

**Q**: `Now instead of reading the message from the result const, I want to retrieve it from my api using the `useFetch` composable that comes with Nuxt3 - I have an endpoint /api/chat-completion that takes the description ref in body Here is some documentation on the useFetch composable - {{ NUXT_3_USE_FETCH_DOCS }}`

*NOTE: At the `NUXT_3_USE_FETCH_DOCS` I have copy pasted the crucial parts of `useFetch` documentation from official Nuxt3 docs, to try to teach ChatGPT how to use it, so can give me a viable result this time.*

**A**: `You can use the useFetch composable in your Vue component to fetch the message from the /api/chat-completion endpoint by sending the description ref in the request body. Here is an example of how you can modify your component to achieve this:`

```html
<script setup lang="ts">
import { ref } from 'vue';
import { useFetch } from 'nuxt3';

const title = ref('');
const description = ref('');
const image = "https://thumbs.dreamstime.com/b/pizza-rustic-italian-mozzarella-cheese-basil-leaves-35669930.jpg";
const message = ref('');

const submitPost = async (): Promise<void> => {
  // Process the form data here
  console.log('Title:', title.value);
  console.log('Description:', description.value);

  // Fetch the message from the API
  const { data } = await useFetch('/api/chat-completion', {
    method: 'POST',
    body: { description: description.value },
  });
  message.value = data.message;
};
</script>

<template>
  <!-- Your existing template content -->
  
  <!-- Social Media Card section -->
  <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 w-full md:w-2/3 lg:w-1/2 mx-auto" v-if="message">
    <div class="space-y-4">
      <div class="text-center">
        <img class="w-full h-64 object-cover rounded-md mb-4" :src="image" alt="Social media card preview image">
      </div>
      <div>
        <h2 class="text-2xl font-bold mb-2">{{ title }}</h2>
        <p class="text-gray-700 whitespace-pre-line">{{ message }}</p>
      </div>
    </div>
  </div>
</template>
```

`In the <script setup> section, I have imported useFetch from 'nuxt3' and created a new ref message. In the submitPost function, I'm calling useFetch with the /api/chat-completion endpoint and sending the description in the request body. Then, I set the value of the message ref to the fetched message data.`

`In the template, I added the v-if="message" directive to the social media card section, so it will only be displayed when the message has been fetched. The message is displayed using the {{ message }} binding.`
