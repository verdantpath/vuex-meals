<template>
  <a 
    :href="href" 
    target="_blank" 
    class="px-3 py-2 text-white bg-orange-500 rounded border-2 border-orange-600 hover:bg-orange-600 hover:text-white transition-colors"
  >
    <slot>YouTube</slot>
  </a>
</template>
<script setup>
  const props = defineProps({
    href: String
  })
</script>
<style>

</style>