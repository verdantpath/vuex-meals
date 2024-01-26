<template>
  <div class="p-8 pb-0">
    <input 
      type="text" 
      v-model="keyword"
      class="rounded border-2 border-gray-200 w-full" 
      placeholder="Search for Meals" 
      @change="searchMeals"
    />
  </div>
  <div class="grid grid-cols-1 md:grid-cols-3 gap-5 p-8">
    <MealItem v-for="meal of meals" :key="meal.idMeal" :meal="meal" />
  </div>
</template>
<script setup>
import { ref, onMounted } from 'vue';
import { computed } from "@vue/reactivity";
import store from '../store';
import { useRouter, useRoute } from 'vue-router';
import YouTubeButton from "../components/YouTubeButton.vue"
import MealItem from "../components/MealItem.vue";

const router = useRouter();
const route = useRoute();
const keyword = ref('');
const meals = computed(() => store.state.searchedMeals)

function searchMeals() {
  store.dispatch('searchMeals', keyword.value)
  router.push({ path: `/by-name/${keyword.value}` })
}

onMounted(() => {
  keyword.value = route.params.name
  if (keyword.value) {
    searchMeals();
  }
});

</script>