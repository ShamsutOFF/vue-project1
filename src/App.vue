<script setup>

import MainButton from "@/components/MainButton.vue";
import Header from "@/components/Header.vue";
</script>

<template>
  <Header/>
  <main>
    <MainButton>Начать игру</MainButton>
  </main>
</template>

<style scoped>
main {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 120px;
}
</style>
