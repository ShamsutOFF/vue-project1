<script setup>
import IconLocation from "@/icons/IconLocation.vue";
import Button from "@/components/Button.vue";

function log() {
  console.log("log function called");
}
</script>

<template>
  <Button @click="log">
    <template #icon>
      <IconLocation/>
    </template>
    Изменить город
  </Button>
  <input />
  <Button>
    Сохранить
  </Button>
</template>

<style scoped>

</style>