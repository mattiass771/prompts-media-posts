# Vue Component creation

## 1st prompt

I provided it with basic instructions on how I want my website to look and what frameworks I am using.

**Q**: `Hello ChatGPT, you are my helpful assistant. I am going to create a website in Nuxt 3, that will be able to generate posts for social media. I have my Nuxt project already setup, and I want you to create a Vue component that will contain an input type text for the title of the social media post, a textarea for the description of the social media post and a submit button. I want you to use tailwindcss for styling and I want my accent color to be #41B883. Add a nice light background color that suits my accent color.`  

**A**: `Hello! I'm happy to help you create a Vue component for your Nuxt 3 project. Here's a sample component code that should meet your requirements:`
```html
<template>
  <div class="min-h-screen bg-gray-100 flex items-center justify-center">
    <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 w-full max-w-md">
      <form @submit.prevent="submitPost" class="space-y-4">
        <div>
          <label class="block text-gray-700 text-sm font-bold mb-2" for="title">
            Title
          </label>
          <input
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
            id="title"
            v-model="title"
            type="text"
            placeholder="Enter post title"
          />
        </div>
        <div>
          <label class="block text-gray-700 text-sm font-bold mb-2" for="description">
            Description
          </label>
          <textarea
            class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline h-32 resize-none"
            id="description"
            v-model="description"
            placeholder="Enter post description"
          ></textarea>
        </div>
        <div class="flex items-center justify-end">
          <button
            class="bg-accent hover:bg-accent-light text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
            type="submit"
          >
            Submit
          </button>
        </div>
      </form>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      description: "",
    };
  },
  methods: {
    submitPost() {
      // Process the form data here
      console.log("Title:", this.title);
      console.log("Description:", this.description);
    },
  },
};
</script>

<style scoped>
.bg-accent {
  background-color: #41b883;
}
.bg-accent-light {
  background-color: #63d5a3;
}
</style>
```

*I wasn’t quite happy with the result, since it was written in Options API and I am a fan of the Composition API Vue 3 offers, so I gave him a followup request to transform the code*

## 2nd prompt

**Q**: `Transform the Vue component to Composition API with Typescript support please. Regarding styling, can you also please add some more styling, smoothening the elements, centering them in the viewport and adding some rounded edges with some box-shadow?`  

**A**: `Sure! I have converted the Vue component to use Composition API and Typescript. This version of the component has a smooth, page-wide layout with elements centered horizontally. The width of the form is adjusted based on the viewport size, and the form is centered using the mx-auto utility class. I've also added a heading for the form and adjusted the form's margins for a better visual appearance. Here's the updated code:`
```html
<script setup lang="ts">
import { ref } from 'vue';

const title = ref('');
const description = ref('');

const submitPost = (): void => {
  // Process the form data here
  console.log('Title:', title.value);
  console.log('Description:', description.value);
};
</script>

<style scoped>
.bg-accent {
  background-color: #41b883;
}
.bg-accent-light {
  background-color: #63d5a3;
}
</style>

<template>
  <div class="min-h-screen bg-gray-100 flex items-center">
    <div class="container mx-auto px-4">
      <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 w-full md:w-2/3 lg:w-1/2 mx-auto">
        <h2 class="text-2xl font-bold text-center mb-6">Create a Social Media Post</h2>
        <form @submit.prevent="submitPost" class="space-y-4">
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2" for="title">
              Title
            </label>
            <input
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
              id="title"
              v-model="title"
              type="text"
              placeholder="Enter post title"
            />
          </div>
          <div>
            <label class="block text-gray-700 text-sm font-bold mb-2" for="description">
              Description
            </label>
            <textarea
              class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline h-32 resize-none"
              id="description"
              v-model="description"
              placeholder="Enter post description"
            ></textarea>
          </div>
          <div class="flex items-center justify-center">
            <button
              class="bg-accent hover:bg-accent-light text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
              type="submit"
            >
              Submit
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
```

*This was a very good result after 2 prompts, and I was surprised how tidy and smooth it looked.*