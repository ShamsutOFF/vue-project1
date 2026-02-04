<script setup>
import Stat from "@/components/Stat.vue";
import CitySelect from "@/components/CitySelect.vue";
import {computed, onMounted, ref} from "vue";

const API_ENDPOINT = "https://api.weatherapi.com/v1";
const apiKey = import.meta.env.VITE_API_KEY

let savedCity = ref("Moscow");
let data = ref({
  humidity: "75%",
  temperature: "20°C",
  wind: "10 м/с"
});

onMounted(() => {
  getCity(savedCity.value);
});

const dataModified = computed(() => {
  return [
    {
      label: "Влажность",
      stat: data.value.humidity
    },
    {
      label: "Температура",
      stat: data.value.temperature
    },
    {
      label: "Ветер",
      stat: data.value.wind
    }];
});

async function getCity(city) {
  const params = new URLSearchParams({
    query: city,
    key: apiKey,
    lang: "ru",
    days: 3
  });
  const response = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`)
  const data = await response.json();
  console.log(data);
  savedCity.value = data.location.name;
}

</script>

<template>
  <main class="main">
    <div id="city">{{ savedCity }}</div>
    <Stat v-for="item in dataModified" v-bind="item" :key="item.label"/>
    <CitySelect @select-city="getCity"/>
  </main>
</template>

<style scoped>
.main {
  background: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
}
</style>
