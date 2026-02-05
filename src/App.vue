<script setup>
import Stat from "@/components/Stat.vue";
import CitySelect from "@/components/CitySelect.vue";
import Error from "@/components/Error.vue";
import { computed, onMounted, ref } from "vue";

const API_ENDPOINT = "https://api.weatherapi.com/v1";
const apiKey = import.meta.env.VITE_API_KEY;

const errorMap = new Map([
  [1006, "Указанный город не найден"]
]);

const errorDisplay = computed(() => {
  return errorMap.get(error.value?.error?.code) || "Произошла ошибка";
});

let savedCity = ref("Moscow");
let data = ref({
  humidity: "—",
  temperature: "—",
  wind: "—"
});
let error = ref(null);

onMounted(() => {
  getCity(savedCity.value);
});

const dataModified = computed(() => {
  // Всегда возвращаем массив, даже если data.value пустой
  return [
    {
      label: "Температура",
      stat: data.value?.temperature || "—"
    },
    {
      label: "Влажность",
      stat: data.value?.humidity || "—"
    },
    {
      label: "Ветер",
      stat: data.value?.wind || "—"
    }
  ];
});

async function getCity(city) {
  const params = new URLSearchParams({
    query: city,
    key: apiKey,
    lang: "ru",
    days: 3
  });

  try {
    const response = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`);

    if (!response.ok) {
      error.value = await response.json();
      data.value = {};
      return; // Не обнуляем data, показываем старые значения
    }

    error.value = null;
    const resData = await response.json();

    data.value.humidity = resData.current.humidity + "%";
    data.value.temperature = resData.current.temp_c + "°C";
    data.value.wind = resData.current.wind_kph + " км/ч";
    savedCity.value = resData.location.name;

  } catch (err) {
    error.value = { error: { code: 1006 } };
    console.error("Ошибка запроса:", err);
  }
}
</script>

<template>
  <main class="main">
    <Error v-if="error" :error="errorDisplay"/>
    <div v-if="!error" id="city">{{ savedCity }}</div>
    <!-- dataModified всегда будет массивом -->
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
