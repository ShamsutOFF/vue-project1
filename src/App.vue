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
      label: "Температура",
      stat: data.value.temperature
    },
    {
      label: "Влажность",
      stat: data.value.humidity
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
  const resData = await response.json();
  console.log(resData);
  data.value.humidity = resData.current.humidity + "%";
  data.value.temperature = resData.current.temp_c + "°C";
  data.value.wind = resData.current.wind_kph + " м/с";
  savedCity.value = resData.location.name;
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
