<script setup>
import {onMounted, ref} from "vue";
import PaneRight from "@/components/PaneRight.vue";

const API_ENDPOINT = "https://api.weatherapi.com/v1";
const apiKey = import.meta.env.VITE_API_KEY;


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
    <div class="left">

    </div>
    <div class="right">
      <PaneRight
          :data="data"
          :error="error"
          :active-index="activeIndex"
          @select-index="(index) => activeIndex = index"
          @select-city="(city) => getCity(city)"
      />
    </div>
  </main>
</template>

<style scoped>
.main {
  display: flex;
  align-items: center;
  justify-content: center;
}

.left {
  width: 500px;
  height: 640px;
  border-radius: 30px;
  background-image: url("./assets/bg.png");
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}

.right {
  background: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 0 25px 25px 0;
  display: flex;
  flex-direction: column;
  gap: 70px;
}
</style>