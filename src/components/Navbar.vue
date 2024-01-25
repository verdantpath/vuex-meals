<template>
  <header class="bg-white shadow h-16 flex justify-between items-stretch">
      <router-link :to="{name: 'home'}" class="inline-flex items-center px-5 h-full">
        Home
      </router-link>
      <div class="flex items-center gap-1">
        <router-link :to="{name: 'byName'}" class="inline-flex items-center px-2 h-full hover:bg-purple-200">
          Search Meals
        </router-link>
        <router-link :to="{name: 'byLetter'}" class="inline-flex items-center px-2 h-full hover:bg-purple-200">
          Search By Letter
        </router-link>
        <router-link :to="{name: 'ingredients'}" class="inline-flex items-center px-2 h-full hover:bg-purple-200">
          Meals By Ingredient
        </router-link>
      </div>
    </header>
</template>
<script>
  export default {
    
  }
</script>
<style>

</style>