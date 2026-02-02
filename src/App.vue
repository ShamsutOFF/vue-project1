<script setup>
import Button from "@/components/Button.vue";
import Stat from "@/components/Stat.vue";
import IconLocation from "@/icons/IconLocation.vue";

const data = {
  label: "ВЛАЖНОСТЬ",
  stat: "90%"
}
</script>

<template>
  <main class="main">
    <Stat v-bind="data"></Stat>
    <Stat label="ОСАДКИ" stat="0%"></Stat>
    <Button>
      <template #icon>
        <IconLocation/>
      </template>
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
