<script setup>

const emit = defineEmits(['new-game']);

const handleClick = () => {
  emit('new-game');
}

</script>

<template>
  <button class="button" @click="handleClick">
    <slot/>
  </button>
</template>

<style scoped>
.button {
  border: none;
  border-radius: 100px;
  padding: 16px 10px;
  background-color: var(--color-blue-button);
  color: var(--color-white);
  min-width: 335px;
  font-size: 24px;
  font-weight: 400;
  line-height: 1.2;
  text-align: center;
  cursor: pointer;
}

.button:hover {
  background-color: var(--color-blue-button-hover);
}
</style>