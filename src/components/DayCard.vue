<script setup>
import IconSun from "@/icons/weather/IconSun.vue";
import IconRain from "@/icons/weather/IconRain.vue";
import IconCloud from "@/icons/weather/IconCloud.vue";

const {weatherCode, temperature, date} = defineProps({
  weatherCode: {
    type: String,
    required: true
  },
  temperature: {
    type: Number,
    required: true
  },
  date: {
    type: Date,
    required: true
  }
});
</script>

<template>
  <button class="day-card">
    <IconSun v-if="weatherCode == 1000"/>
    <IconCloud v-if="weatherCode == 1003"/>
    <IconRain v-if="weatherCode == 1009"/>
    <div class="day-card__day">
      {{ date.toLocaleString('ru-RU', {weekday: 'short'}) }}
    </div>
    <div class="day-card__temp">
      {{ temperature + "°C" }}
    </div>
  </button>
</template>

<style scoped>
.day-card {
  background-color: var(--color-bg-card);
  border-radius: 10px;
  border: none;
  cursor: pointer;
  padding: 20px 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 15px;
  color: var(--color-primary);
  box-shadow: 1px 2px 4px 0 #222831;
}

.day-card:hover {
  background-color: var(--color-bg-card-hover);
}

.day-card__day {
  font-size: 20px;
  font-weight: 400;
}

.day-card__temp {
  font-size: 20px;
  font-weight: 700;
}
</style>