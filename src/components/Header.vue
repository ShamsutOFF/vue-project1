<script setup>

import Score from "@/components/Score.vue";
</script>

<template>
  <header>
    <h1>ЗАПОМНИ СЛОВО</h1>
    <Score/>
  </header>
</template>

<style scoped>
header {
  color: var(--color-text-main);
  text-align: center;
  font-size: 16px;
  font-weight: 700;
  line-height: 1.2;
  text-transform: uppercase;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 120px;
  padding: 0 20px;
  max-width: 1200px;
  margin: 0 auto;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  background-color: var(--color-bg-main);
}
</style>