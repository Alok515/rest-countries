<script setup>

const countryData = ref(null)
const isLoading = ref(true)
const { code } = useRoute().params;
console.log(code);
//loades the data on mount
onMounted(async () => {
  const rawData = await fetch(`https://restcountries.com/v3.1/alpha/${code}`)
  const parsedData = await rawData.json()
  countryData.value = parsedData
  isLoading.value = false
})
</script>

<template>
  <div class="bg-white">
    <div v-if="isLoading" class="h-screen flex justify-center items-center">
      <LoadingSpinner />
    </div>
    <div v-else>
      <CountryDetails :data="countryData" />
    </div>
  </div>
</template>