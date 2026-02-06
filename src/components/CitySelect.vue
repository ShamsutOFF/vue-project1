<script setup>
import IconLocation from "@/icons/IconLocation.vue";
import Button from "@/components/Button.vue";
import {ref} from "vue";
import Input from "@/components/Input.vue";

const emit = defineEmits({
  selectCity(payload) {
    return payload;
  },
});

let city = ref("Moscow");
let isEdited = ref(false);

function select() {
  isEdited.value = false;
  emit("selectCity", city.value);
}

function edit() {
  isEdited.value = true;
}

</script>

<template>
  <div class="city-select">
    <div v-if="isEdited" class="city-input">
      <Input
          v-model="city"
          v-focus
          placeholder="Введите город"
          @keyup.enter="select"/>
      <Button @click="select">Сохранить</Button>
    </div>
    <Button v-else @click="edit()">
      <template #icon>
        <IconLocation/>
      </template>
      Изменить город
    </Button>
  </div>
</template>

<style scoped>
.city-input {
  display: flex;
  align-items: center;
  gap: 12px;
}

.city-select {
  width: 420px;
}
</style>