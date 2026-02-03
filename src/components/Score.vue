<script setup>

import IconHeart from "@/components/Icons/IconHeart.vue";
</script>

<template>
  <div class="score_card">
    <span>100</span>
    <IconHeart></IconHeart>
  </div>
</template>

<style scoped>
.score_card {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 10px;
  color: var(--color-blue-button);
  text-align: center;
  font-size: 16px;
  font-weight: 700;
  line-height: 1.2;
  border-radius: 36px;
  background-color: var(--color-light-blue);
  padding: 12px 24px;
}
</style>