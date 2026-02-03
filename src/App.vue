<script setup>

import MainButton from "@/components/MainButton.vue";
import Header from "@/components/Header.vue";
import GameCard from "@/components/GameCard.vue";
</script>

<template>
  <Header/>
  <div class="content">
    <GameCard/>
    <main>
      <MainButton>Начать игру</MainButton>
    </main>
  </div>
</template>

<style scoped>
.content {
  padding-top: 120px;
  display: flex;
  flex: 1;
  gap: 120px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 120px;
}

</style>
