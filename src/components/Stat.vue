<script setup>
const {label = "Не задано", stat = "0%"} = defineProps({
  label: String,
  stat: String
})
// Старый подход:
// const defProps = withDefaults(defineProps({
//   label: String,
//   stat: String
// }), { label : "No def val"});
</script>

<template>
  <div class="stat">
    <div class="stat-name">{{ label }}</div>
    <div class="stat-value">{{ stat }}</div>
  </div>
</template>

<style scoped>
.stat {
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  font-size: 28px;
  font-weight: 700;
  gap: 16px;
}

.stat-value {
  font-weight: 500;
}
</style>