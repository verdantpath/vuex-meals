<template>
  <div class="max-w-[800px] mx-auto p-8">
    <h1 class="text-4xl font-bold mb-5 text-orange-500">{{ meal.strMeal }}</h1>
    <img :src="meal.strMealThumb" :alt="meal.strMeal" class="max-w-full">
    <div class="grid grid-cols-1 sm:grid-cols-3 text-lg py-2">
      <div>
        <strong class="font-bold">Category:</strong> {{ meal.strCategory }}
      </div>
      <div>
        <strong class="font-bold">Area:</strong> {{ meal.strArea }}
      </div>
      <div>
        <strong class="font-bold">Tags:</strong> {{ meal.strTags }}
      </div>
    </div>

     <div class="my-3">
      {{ meal.strInstructions }}
     </div>

    <div class="grid grid-cols-1 sm:grid-cols-2">
      <div>
        <h2 class="text-2xl font-semibold mb-2">Ingredients</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)" :key="ind">
            <li v-if="meal[`strIngredient${ind + 1}`]">
              <span>{{ ind + 1 }}.</span> 
              {{ meal[`strIngredient${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>
      <div>
        <h2 class="text-2xl font-semibold mb-3">Measures</h2>
        <ul>
          <template v-for="(el, ind) of new Array(20)" :key="ind">
            <li v-if="meal[`strMeasure${ind + 1}`]">
              <span>{{ ind + 1 }}.</span> 
              {{ meal[`strMeasure${ind + 1}`] }}
            </li>
          </template>
        </ul>
      </div>

      <div class="mt-4">
        <YouTubeButton :href="meal.strYoutube">Go To YouTube</YouTubeButton>
        <a 
          :href="meal.strSource" 
          target="_blank" 
          class="ml-3 px-3 py-2 text-indigo-600 border-2 border-transparent rounded transition-colors"
        >
          View Original Source
        </a>
      </div>
    </div>

  </div>
</template>
<script setup>
  import { ref, onMounted } from 'vue';
  import {useRoute } from 'vue-router';
  import axiosClient from '../axiosClient';
  import YouTubeButton from '../components/YouTubeButton.vue';

  const route = useRoute();
  const meal = ref({})

  onMounted(() => {
    axiosClient.get(`lookup.php?i=${route.params.id}`)
      .then(({ data }) => {
        // debugger;
        meal.value = data.meals[0] || {}
      })
  });

</script>
<style>

</style>