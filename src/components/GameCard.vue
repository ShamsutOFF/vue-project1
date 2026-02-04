<script setup>
import { computed } from 'vue'

const props = defineProps({
  card: {
    type: Object,
    required: true
  }
})

const emit = defineEmits(['flip', 'answer'])

const isClickable = computed(() => props.card.status === 'default')
const isFlipped = computed(() => props.card.status !== 'default')
const showButtons = computed(() => props.card.status === 'flipped')
const isFinished = computed(() =>
    props.card.status === 'correct' || props.card.status === 'incorrect'
)

const handleCardClick = () => {
  if (isClickable.value) {
    emit('flip', props.card.id)
  }
}

const handleYes = () => {
  emit('answer', props.card.id, true)
}

const handleNo = () => {
  emit('answer', props.card.id, false)
}
</script>

<template>
  <div
      class="card-wrapper"
      :class="{ flipped: isFlipped, clickable: isClickable }"
      @click="handleCardClick"
  >
    <!-- Лицевая сторона -->
    <div class="card card-front" :class="`status-${card.status}`">
      <div v-if="isFinished" class="result-icon">
        <div class="icon-badge" :class="card.status === 'correct' ? 'badge-success' : 'badge-error'">
          <span v-if="card.status === 'correct'">✓</span>
          <span v-else>✗</span>
        </div>
      </div>

      <div class="card-header">
        <div class="card-number">{{ card.number }}</div>
      </div>

      <div class="card-content">
        <div class="card-text">{{ card.word }}</div>
      </div>

      <div class="card-footer">
        <div v-if="isFinished">ЗАВЕРШЕНО</div>
        <div v-else>ПЕРЕВЕНУТЬ</div>
      </div>
    </div>

    <!-- Обратная сторона -->
    <div class="card card-back" :class="`status-${card.status}`">
      <div v-if="isFinished" class="result-icon">
        <div class="icon-badge" :class="card.status === 'correct' ? 'badge-success' : 'badge-error'">
          <span v-if="card.status === 'correct'">✓</span>
          <span v-else>✗</span>
        </div>
      </div>

      <div class="card-header">
        <div class="card-number">{{ card.number }}</div>
      </div>

      <div class="card-content">
        <div class="card-text">{{ card.translation }}</div>
      </div>

      <div class="card-footer">
        <div v-if="showButtons" class="answer-buttons">
          <button @click.stop="handleNo" class="btn-icon btn-error">
            <span>✗</span>
          </button>
          <button @click.stop="handleYes" class="btn-icon btn-success">
            <span>✓</span>
          </button>
        </div>
        <div v-else-if="isFinished">ЗАВЕРШЕНО</div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card-wrapper {
  width: 250px;
  height: 380px;
  position: relative;
  transform-style: preserve-3d;
  transition: transform 0.6s;
}

.card-wrapper.clickable:hover {
  cursor: pointer;
}

.card-wrapper.flipped {
  transform: rotateY(180deg);
}

.card {
  width: 100%;
  height: 100%;
  border-radius: 16px;
  background-color: var(--color-white);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: center;
  position: absolute;
  backface-visibility: hidden;
  box-shadow: 0 0 16px 0 #0000001A;
  transition: box-shadow 0.3s ease;
}

.card-front {
  z-index: 2;
  transform: rotateY(0deg);
}

.card-back {
  transform: rotateY(180deg);
}

.card-wrapper.clickable:hover .card {
  box-shadow: 10px 10px 10px 0 #0000000D;
}

.card::before {
  content: '';
  position: absolute;
  top: 27px;
  left: 19px;
  right: 19px;
  bottom: 27px;
  border: 1px solid var(--color-light-blue);
  border-radius: 8px;
  pointer-events: none;
  z-index: 1;
  transition: border-color 0.3s ease;
}

.card.status-correct::before {
  border-color: var(--color-success, #22c55e);
}

.card.status-incorrect::before {
  border-color: var(--color-error, #ef4444);
}

.result-icon {
  position: absolute;
  top: 10px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 3;
}

.icon-badge {
  width: 36px;
  height: 36px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 28px;
  font-weight: bold;
  color: white;
}

.badge-success {
  background-color: var(--color-success, #22c55e);
}

.badge-error {
  background-color: var(--color-error, #ef4444);
}

.card-header {
  width: 100%;
  text-align: left;
  position: relative;
  z-index: 2;
  box-sizing: border-box;
  padding-left: 32px;
  padding-top: 16px;
}

.card-number {
  background-color: var(--color-white);
  font-size: 14px;
  padding: 2px;
  line-height: 100%;
  font-weight: 400;
  color: var(--color-text-main);
  display: inline-block;
}

.card-content {
  flex: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  position: relative;
  z-index: 2;
}

.card-text {
  font-size: 18px;
  text-align: center;
  line-height: 100%;
  font-weight: 400;
  color: var(--color-text-main);
}

.card-footer {
  background-color: var(--color-white);
  padding-bottom: 18px;
  padding-left: 4px;
  padding-right: 4px;
  text-align: center;
  font-weight: 700;
  font-size: 12px;
  line-height: 18px;
  letter-spacing: 2px;
  color: var(--color-text-main);
  position: relative;
  z-index: 2;
}

.answer-buttons {
  display: flex;
  gap: 12px;
  justify-content: center;
}

.btn-icon {
  width: 24px;
  height: 24px;
  border: none;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: opacity 0.2s, transform 0.2s;
  font-size: 16px;
  font-weight: bold;
  color: white;
  padding: 0;
}

.btn-success {
  background-color: var(--color-success, #22c55e);
}

.btn-error {
  background-color: var(--color-error, #ef4444);
}

.btn-icon:hover {
  opacity: 0.8;
  transform: scale(1.1);
}

.btn-icon:active {
  transform: scale(0.95);
}
</style>
