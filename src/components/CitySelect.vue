<script setup>
import IconLocation from "@/icons/IconLocation.vue";
import Button from "@/components/Button.vue";
import {inject, ref, watch} from "vue";
import Input from "@/components/Input.vue";

// Получаем реактивную ссылку
const city = inject("city")

// Локальное состояние для input
const inputValue = ref(city.value) // Начальное значение

// Следим за изменениями city и синхронизируем inputValue
watch(city, (newVal) => {
  inputValue.value = newVal
})

let isEdited = ref(false);

function select() {
  isEdited.value = false;
  city.value = inputValue.value; // Изменяем реактивное значение
}

function edit() {
  isEdited.value = true;
}

</script>

<template>
  <div class="city-select">
    <div v-if="isEdited" class="city-input">
      <Input
          v-model="inputValue"
          placeholder="Введите город"
          @keyup.enter="select"/>
      <Button @click="select">Сохранить</Button>
    </div>
    <Button v-else @click="edit">
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