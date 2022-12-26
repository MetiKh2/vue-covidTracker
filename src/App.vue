<script setup>
import { onMounted, ref, watch } from 'vue';
import Header from './components/Header.vue'
import CartBoxes from './components/CartBoxes.vue'
import Countries from './components/Countries.vue'

let stats = ref({})
let countries = ref([])
let apiResult={};
async function fetchCovidData() {
  const res = await fetch('https://api.covid19api.com/summary')
  return await res.json();
}
onMounted(async () => {
  apiResult = await fetchCovidData();
  stats.value = apiResult.Global
  countries.value = apiResult.Countries
  console.log(apiResult);
})
function countryChanged(countryId) {
  if (parseInt(countryId) == 0) {
    stats.value=apiResult.Global
  }
  else {
    const country = countries.value.find((item) => item.ID === countryId);
    stats.value = country
  }
}
</script>

<template>
  <Header />
  <div class="text-center mb-5">
    <h3 class="font-bold text-3xl">Global</h3>
    <p class="mt-3 font-bold">{{ new Date() }}</p>
  </div>
  <CartBoxes :stats.sync="stats" />
  <Countries :countries.sync="countries" @countryChanged="countryChanged" />
</template>

<style scoped>

</style>
