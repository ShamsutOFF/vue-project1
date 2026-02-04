<script setup>
import Stat from "@/components/Stat.vue";
import CitySelect from "@/components/CitySelect.vue";
import {computed, ref} from "vue";

let savedCity = ref("Moscow");
let data = ref({
  humidity: "75%",
  temperature: "20°C",
  wind: "10 м/с"
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
  savedCity.value = city;
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
