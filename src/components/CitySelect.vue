<script setup>
import IconLocation from "@/icons/IconLocation.vue";
import Button from "@/components/Button.vue";
</script>

<template>
  <Button>
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