<script setup>
</script>

<template>
  <button class="button">
    <span>
      <slot name="icon"/>
    </span>
    <slot/>
  </button>
</template>

<style scoped>
.button {
  border: none;
  border-radius: 10px;
  background: var(--gradent);
  padding: 14px;
  font-family: var(--font), sans-serif;
  font-size: 20px;
  color: var(--color-primary);
  cursor: pointer;
}

.button:hover {
  background: var(--gradent-inverted);
}

</style>