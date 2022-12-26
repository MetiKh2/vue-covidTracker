<script setup>
import { ref, watch } from 'vue';

let {countries,countryChanged}=defineProps(['countries','countryChanged'])
let selected=ref(0)
const emit = defineEmits(['countryChanged'])
function onChange() {
    // const country = countries.find((item) => item.ID === selected.value);
        // emit('countryChanged', country);
        // console.log(countries,'dkdkdssk');
        emit('countryChanged',selected.value) 
}

</script>
<template>
    <select v-model="selected" class="form-select mt-10 block w-full border p-3 rounded" @change="onChange()">
        <option value="0">Global</option>
        <option v-for="country in countries" :value="country.ID">
            {{ country.Country }}
        </option>
    </select>
</template>