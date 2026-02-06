<script setup>
import Stat from "@/components/Stat.vue";
import CitySelect from "@/components/CitySelect.vue";
import Error from "@/components/Error.vue";
import {computed, onMounted, ref} from "vue";
import DayCard from "@/components/DayCard.vue";

const API_ENDPOINT = "https://api.weatherapi.com/v1";
const apiKey = import.meta.env.VITE_API_KEY;

const errorMap = new Map([
  [1006, "Указанный город не найден"]
]);

const errorDisplay = computed(() => {
  return errorMap.get(error.value?.error?.code) || "Произошла ошибка";
});

let savedCity = ref("Казань");
let data = ref({
  humidity: "—",
  temperature: "—",
  wind: "—",
  forecast: []
});
let error = ref(null);
let activeIndex = ref(0);

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
    days: 4
  });

  try {
    const response = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`);

    if (!response.ok) {
      error.value = await response.json();
      data.value = {
        humidity: "—",
        temperature: "—",
        wind: "—",
        forecast: []
      };
      return;
    }
    error.value = null;
    const resData = await response.json();
    // console.log(resData);

    // Сохраняем текущую погоду
    data.value.humidity = resData.current.humidity + "%";
    data.value.temperature = resData.current.temp_c + "°C";
    data.value.wind = resData.current.wind_kph + " км/ч";

    // Сохраняем прогноз!
    data.value.forecast = resData.forecast?.forecastday || [];

    savedCity.value = resData.location.name;

  } catch (err) {
    error.value = {error: {code: 1006}};
    console.error("Ошибка запроса:", err);
  }
}
</script>

<template>
  <main class="main">
    <Error v-if="error" :error="errorDisplay"/>

    <!-- Статистика -->
    <div class="stats-section">
      <Stat
          v-for="item in dataModified"
          v-bind="item"
          :key="item.label"
      />
    </div>

    <!-- Прогноз с карточками -->
    <div
        v-if="data && data.forecast && data.forecast.length > 0"
        class="forecast-section"
    >
      <div class="day-card-list">
        <DayCard
            v-for="(item, index) in data.forecast"
            :key="item.date"
            :date="new Date(item.date)"
            :temperature="item.day.avgtemp_c"
            :weather-code="item.day.condition.code"
            :is-active="activeIndex === index"
            @click="activeIndex = index"
        />
      </div>
    </div>

    <!-- Выбор города -->
    <div class="city-select-section">
      <CitySelect @select-city="getCity"/>
    </div>
  </main>
</template>

<style scoped>
.main {
  background: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
  display: flex;
  flex-direction: column;
  gap: 70px;
}

/* Секция прогноза */
.forecast-section {
  width: 100%;
}

.day-card-list {
  width: 420px; /* Фиксированная ширина как у CitySelect */
  display: flex;
  gap: 1px; /* или нужное расстояние */
  justify-content: space-between; /* равномерное распределение */
}

:deep(.day-card) {
  flex: 1; /* Растягиваются равномерно */
  min-width: 0; /* Важно для корректного сжатия текста */
}

/* Секция выбора города */
.city-select-section {
  display: flex;
  justify-content: center;
}
</style>