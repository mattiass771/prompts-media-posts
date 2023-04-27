# API With Openai Client Setup

## 1st Prompt

**Q**: `Now I want you to create an event handler in my Nuxt3 server. It has to read a message from the request body, and use it as a prompt for the ChatCompletition module of openai nodejs library and return the result as a response. I want to use the gpt-3-turbo model.`

*Since ChatGPT doesn’t know the Nuxt3 syntax yet, it provided me a solution for Nuxt.js which is an older version. Nevertheless the code was still easily adaptable, but I had to do this bit myself. I am sure that if I have chosen a framework ChatGPT knows, I wouldn't have to adapt anything but the openai syntax, which was also a bit outdated.  

Nevertheless, I am going to show you the original response that it provided me. Since Nuxt3 comes with useFetch hook, we also don’t have to install the axios package.*

**A**: `To create an event handler in your Nuxt 3 server, you can create a server route. First, you need to install the OpenAI Node.js package:`

```bash
npm install openai
```
`Create a new file called chat_completion.ts in the server/api directory of your Nuxt 3 project:`

```typescript
// server/api/chat_completion.ts

import { defineServerRoute } from '@nuxt/server';
import openai from 'openai';

openai.apiKey = 'your_openai_api_key'; // Replace with your actual API key

export default defineServerRoute(async (app) => {
  app.post('/chat_completion', async (req, res) => {
    const prompt = req.body.message;

    if (!prompt) {
      res.status(400).json({ error: 'Message is required' });
      return;
    }

    try {
      const response = await openai.Completion.create({
        engine: 'text-davinci-002',
        prompt,
        max_tokens: 50, // Adjust the number of tokens to your desired output length
        n: 1,
        stop: null,
        temperature: 0.5,
      });

      const result = response.choices[0].text.trim();

      res.status(200).json({ message: result });
    } catch (error) {
      console.error('Error during ChatCompletion:', error);
      res.status(500).json({ error: 'An error occurred while processing your request' });
    }
  });
});
```

`In this server route, I've created a POST endpoint at /chat_completion. It reads the message from the request body, and then it uses the message as a prompt for the ChatCompletion module from the OpenAI Node.js library. The result is returned as a response.`

`Replace 'your_openai_api_key' with your actual OpenAI API key. You can adjust the parameters of the openai.Completion.create() function to suit your needs, such as max_tokens, n, stop, and temperature.`

`Finally, you can call this endpoint from your Vue component when submitting the form:`

```tsx
// Add this import at the top of your component file
import axios from 'axios';

// Replace the submitPost function with this one
const submitPost = async (): Promise<void> => {
  // Process the form data here
  console.log('Title:', title.value);
  console.log('Description:', description.value);

  try {
    const response = await axios.post('/api/chat_completion', { message: description.value });
    console.log('Generated Text:', response.data.message);
  } catch (error) {
    console.error('Error during chat completion:', error);
  }
};`
```

`Make sure to have axios installed in your project:`

```bash
npm install axios
```

`With these changes, your component will now call the /api/chat_completion endpoint with the description value when the form is submitted. The generated text from GPT-3 will be logged in the console.`

`Note that using GPT-3 might incur costs depending on your usage. Be cautious with the number of API calls you make to avoid unexpected charges.`