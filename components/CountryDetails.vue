<script setup>
import { ArrowLeftIcon } from '@heroicons/vue/20/solid'

// eslint-disable-next-line no-unused-vars
const { data } = defineProps(['data'])

//geting keys for dynamicly accessing properties
const borders = ref(data[0].borders)
const languages = ref(Object.values(data[0].languages))
const keyIndex = languages.value.length > 1 ? 1 : 0
const nativeLangIndex = ref(languages.value[keyIndex])
const currencieKeys = ref(Object.keys(data[0].currencies))
</script>

<template>
  <div class="p-12 max-sm:p-4 max-md:p-8">
    <div class="mb-8 w-32 bg-gray-100">
      <NuxtLink
        to="/"
        class="flex gap-4  items-center pl-4 pr-8 py-1 shadow-xl transition duration-200 hover:shadow-md"
      >
        <ArrowLeftIcon class="h-8 w-8"/>
        <p>Back</p>
      </NuxtLink>
    </div>
    <div
      class="grid grid-cols-2 gap-20 items-center max-md:grid-cols-1 justify-center max-lg:gap-6"
    >
      <div class="w-100%">
        <img :src="data[0].flags.svg" alt="Flag" class="object-cover border" />
      </div>
      <div class="p-8 max-sm:p-2 max-md:p-4">
        <h1 class="text-4xl mb-8 font-bold">{{ data[0].name.common }}</h1>
        <div class="flex justify-between flex-wrap text-sm gap-8">
          <div class="flex flex-col gap-4 flex-nowrap">
            <div class="font-semibold">
              Native Name:
              <span class="text-gray-500 ">{{
                data[0].name?.nativeName[nativeLangIndex]?.common
                  ? data[0].name?.nativeName[nativeLangIndex]?.common
                  : data[0].name.common
              }}</span>
            </div>
            <p class="font-semibold">
              Population: <span class="text-gray-500 ">{{ data[0].population }}</span>
            </p>
            <p class="font-semibold" >
              Region: <span class="text-gray-500 ">{{ data[0].region }}</span>
            </p>
            <p class="font-semibold">
              Sub Region: <span class="text-gray-500 ">{{ data[0].subregion }}</span>
            </p>
            <p class="font-semibold">
              Capital:
              <span class="text-gray-500 ">{{
                data[0]?.capital ? data[0].capital[0] : 'Unkown'
              }}</span>
            </p>
          </div>
          <div class="flex flex-col gap-4">
            <div class="flex items-center gap-2 flex-wrap">
              <p class=" font-semibold">Currencies:</p>

              <div class="flex gap-2 flex-col">
                <p
                  class="text-gray-500 "
                  v-for="currencieKey of currencieKeys"
                  :key="currencieKey"
                  >{{ data[0].currencies[currencieKey].symbol }}-{{
                    data[0].currencies[currencieKey].name
                  }}</p
                >
              </div>
            </div>

            <div class="flex items-center gap-2 flex-wrap">
              <p class=" font-semibold">Languages:</p>
              <div class="">
                <p class="text-gray-500 ">
                  {{ languages.join(', ') }}
                </p>
              </div>
            </div>
          </div>
        </div>
        <div class="mt-8 flex flex-wrap items-center">
          <p class="font-bold mr-2">Borders:</p>
          <div v-if="borders?.length" class="mt-2">
            <p class="flex gap-2 flex-wrap">
              <p
                v-for="border of borders"
                :key="border"
                class="px-4 py-1 bg-white shadow-lg rounded-md text-gray-500 "
              >
                {{ border }}
              </p>
            </p>
          </div>
          <p v-else class=" text-gray-400">No Borders</p>
        </div>
      </div>
    </div>
  </div>
</template>