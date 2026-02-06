<script setup>

import Stat from "@/components/Stat.vue";
import Error from "@/components/Error.vue";
import DayCard from "@/components/DayCard.vue";
import CitySelect from "@/components/CitySelect.vue";
import {computed} from "vue";

const {error, data, activeIndex} = defineProps({
  error: Object,
  data: Object,
  activeIndex: Number
});

const emit = defineEmits(["select-index", "select-city"]);

const errorMap = new Map([
  [1006, "Указанный город не найден"]
]);

const statData = computed(() => {
  // Всегда возвращаем массив, даже если data.value пустой
  return [
    {
      label: "Температура",
      stat: data.temperature || "—"
    },
    {
      label: "Влажность",
      stat: data.humidity || "—"
    },
    {
      label: "Ветер",
      stat: data.wind || "—"
    }
  ];
});

const errorDisplay = computed(() => {
  return errorMap.get(error.error?.code) || "Произошла ошибка";
});

</script>

<template>
  <Error v-if="error" :error="errorDisplay"/>

  <!-- Статистика -->
  <div class="stats-section">
    <Stat
        v-for="item in statData"
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
          @click="() => emit('select-index', index)"
      />
    </div>
  </div>

  <!-- Выбор города -->
  <div class="city-select-section">
    <CitySelect />
  </div>
</template>

<style scoped>

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