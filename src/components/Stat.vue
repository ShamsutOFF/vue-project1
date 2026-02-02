<script setup>

</script>

<template>
  <div class="stat">
    <div class="stat-name">ВЛАЖНОСТЬ</div>
    <div class="stat-value">90%</div>
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
.stat-value{
  font-weight: 500;
}
</style>