<script setup>
import IconLocation from "@/icons/IconLocation.vue";
import Button from "@/components/Button.vue";

const emit = defineEmits({
  selectCity(payload) {
    console.log(payload);
    return payload;
  },
})

function select() {
  emit("selectCity", "London");
}
</script>

<template>
  <Button @click="select()">
    <template #icon>
      <IconLocation/>
    </template>
    Изменить город
  </Button>
  <input/>
  <Button>
    Сохранить
  </Button>
</template>

<style scoped>

</style>