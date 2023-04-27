# The Social Media Card Element

## The Prompt

**Q**:
```
I have added a result const and an image const to my Vue component's script tag: 

const result = { "message": "🍕🚀 Introducing the world's first HEALTHY pizza! Our dough is made with stardust, our tomato sauce has a pinch of moonstone, and our mozzarella is gathered on the Sun. 🌟🌙☀️\n\nWith every bite, our pizza will make you healthier! 😍 Plus, it's DELICIOUS! 🤤\n\nSo why settle for a regular pizza when you can nourish your body with our out-of-this-world creation? Try it out today and experience the intergalactic flavors and surprising health benefits! 😎\n\n#HealthyPizza #OutOfThisWorldFlavor #StardustDough #MoonstoneSauce #SunMozzarella #TryItNow #HealthyEating #IntergalacticCuisine 🍴💪🚀" } 
const image = "https://thumbs.dreamstime.com/b/pizza-rustic-italian-mozzarella-cheese-basil-leaves-35669930.jpg" 

please add another section to the Vue component under the form you have created, so that whenever the message and image are existing, they will be displayed as a social media card
```

**A**: `To add a new section that displays the result and message const as a social media card under the form section, you can modify the template as follows:`

```html
<template>
  <div class="min-h-screen bg-gray-100 flex flex-col items-center">
    <div class="container mx-auto px-4">
      <!-- Form section -->
      <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 w-full md:w-2/3 lg:w-1/2 mx-auto">
        <!-- Existing form content -->
      </div>
      
      <!-- Social Media Card section -->
      <div class="bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 w-full md:w-2/3 lg:w-1/2 mx-auto">
        <div class="space-y-4">
          <div class="text-center">
            <img class="w-full h-64 object-cover rounded-md mb-4" :src="image" alt="Social media card preview image">
          </div>
          <div>
            <h2 class="text-2xl font-bold mb-2">{{ title }}</h2>
            <p class="text-gray-700 whitespace-pre-line">{{ result.message }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
```

`Here, I've added a new <div> with the class "bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4 w-full md:w-2/3 lg:w-1/2 mx-auto" to create a new card section. Inside the card, I've added an image element to display the image variable, and then added a title and description from the title and result.message variables, respectively.`