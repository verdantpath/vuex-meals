<template>
  <div class="p-8 pb-0">
    <h1 class="text-4xl font-bold mb-4 text-orange-500">Search Meals by Name</h1>
  </div>
  <div class="px-8 pb-3">
    <input 
      type="text" 
      v-model="keyword"
      class="rounded border-2 border-gray-200 focus:ring-orange-500 focus:border-orange-500 w-full" 
      placeholder="Search for Meals" 
      @change="searchMeals"
    />
  </div>
  <Meals :meals="meals" />
</template>
<script setup>
import { ref, onMounted } from 'vue';
import { computed } from "@vue/reactivity";
import store from '../store';
import { useRouter, useRoute } from 'vue-router';
import YouTubeButton from "../components/YouTubeButton.vue"
import MealItem from "../components/MealItem.vue";
import Meals from "../components/Meals.vue"

const router = useRouter();
const route = useRoute();
const keyword = ref('');
const meals = computed(() => store.state.searchedMeals)

function searchMeals() {
  if (keyword.value) {
    store.dispatch('searchMeals', keyword.value)
    router.push({ path: `/by-name/${keyword.value}` })
  } else {
    store.commit("setSearchedMeals", []);
    router.push({ path: '/by-name'})
  }
}

onMounted(() => {
  keyword.value = route.params.name
  if (keyword.value) {
    searchMeals();
  }
});

</script>