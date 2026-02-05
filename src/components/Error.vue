<script setup>
const props = defineProps({
  error: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div
      v-if="props.error"
      class="error">
    {{ props.error }}
  </div>
</template>

<style scoped>
.error {
  font-size: 18px;
  padding: 15px;
  text-align: center;
  background: var(--color-bg-card);
  border-radius: 0 0 10px 10px;
  margin-top: -60px;
  margin-bottom: 60px;
}
</style>