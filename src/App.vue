<script setup>
import Button from "@/components/Button.vue";
import Stat from "@/components/Stat.vue";
</script>

<template>
  <main class="main">
    <Stat label="ВЛАЖНОСТЬ" stat="90%"></Stat>
    <Stat label="ОСАДКИ" stat="0%"></Stat>
    <Button>
      Сохранить
    </Button>
  </main>
</template>

<style scoped>
.main {
  background: var(--color-bg-main);
  padding: 60px 50px;
  border-radius: 25px;
}
</style>
