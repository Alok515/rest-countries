<script setup>
// eslint-disable-next-line no-unused-vars
const { country } = defineProps(['country']); 
</script>

<template>
  <div
    class="rounded-lg shadow-lg h-full bg-white transition-all duration-700 hover:scale-105 hover:shadow-2xl"
  >
    <img :src="country.flags.svg" alt="Flag" class="w-full h-[11.5rem] rounded-t-lg object-cover" />
    <div class="p-6">
      <h2 class="font-bold mb-6 text-xl">{{ country.name.common }}</h2>
      <div class="flex gap-2 mb-2">
        <h4 class="font-semibold">Population:</h4> 
        <p class="text-gray-600">{{ country.population }}</p>
      </div>
      <div class="flex gap-2 mb-2">
        <h4 class="font-semibold">Region:</h4> 
        <p class="text-gray-600">{{ country.region }}</p>
      </div>
      <div class="flex gap-2 mb-2">
        <h4 class="font-semibold">Capital:</h4>
        <p class="text-gray-600">{{ country.capital ? country.capital[0] : 'Unkown' }}</p>
      </div>
    </div>
  </div>
</template>