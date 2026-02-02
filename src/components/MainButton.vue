<script setup>

</script>

<template>
  <button class="button">
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