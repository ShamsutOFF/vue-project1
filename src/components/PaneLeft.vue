<script setup>
import {computed, inject} from "vue";
import {cityProvide} from "@/constants.js";
import IconLocation from "@/icons/IconLocation.vue";
import IconRain from "@/icons/weather/IconRain.vue";
import IconSun from "@/icons/weather/IconSun.vue";
import IconCloud from "@/icons/weather/IconCloud.vue";

const {dayData} = defineProps({
  dayData: {
    type: Object,
    required: true
  }
});

const city = inject(cityProvide)

const day = computed(() => {
  return new Date(dayData.date).toLocaleDateString("ru-RU", {
    weekday: "long"
  })
});
const date = computed(() => {
  return new Date(dayData.date).toLocaleDateString("ru-RU", {
    day: "numeric",
    month: "long",
    year: "numeric"
  })
});

const weatherCode = computed(() => {
  return dayData.day.condition.code
})

</script>

<template>
  <div class="pane-left">
    <div>
      <div class="day">
        {{ day }}
      </div>
      <div class="date">
        {{ date }}
      </div>
      <div class="city">
        <IconLocation/>
        {{ city }}
      </div>
    </div>
    <div>
      <div class="weather-icon">
        <IconSun
            v-if="weatherCode <= 1003"
            :size="95"
        />
        <IconCloud
            v-if="weatherCode >= 1006 && weatherCode <= 1063"
            :size="95"
        />
        <IconRain
            v-if="weatherCode >= 1063"
            :size="95"
        />
      </div>
      <div class="temperature">
        {{ dayData.day.avgtemp_c + "°C" }}
      </div>
      <div class="condition">
        {{ dayData.day.condition.text }}
      </div>
    </div>
  </div>
</template>

<style scoped>
.pane-left {
  display: flex;
  flex-direction: column;
  padding: 48px 32px;
  justify-content: space-between;
  height: 100%;
}

.day {
  font-weight: 700;
  font-size: 37px;
  text-transform: capitalize;
  margin-bottom: 16px;
}

.date {
  font-weight: 500;
  font-size: 22px;
  margin-bottom: 10px;
}

.weather-icon {
  margin: 25px;
}

.city {
  display: flex;
  align-items: center;
  gap: 8px;
}

.temperature {
  font-weight: 700;
  font-size: 50px;
  margin-bottom: 9px;
}

.condition {
  font-weight: 500;
  font-size: 30px;
}
</style>