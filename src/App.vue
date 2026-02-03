<script setup>

import MainButton from "@/components/MainButton.vue";
import Header from "@/components/Header.vue";
import GameCard from "@/components/GameCard.vue";
import {ref} from "vue";

const score = ref(100);
// Состояние для карт
const cards = ref([
  {
    id: 1,
    word: 'oscillotron',
    translation: 'осциллотрон',
    state: 'closed', // или 'opened'
    status: 'pending' // 'success' | 'fail' | 'pending'
  },
  {
    id: 2,
    word: 'computer',
    translation: 'компьютер',
    state: 'closed',
    status: 'pending'
  }
  // ... другие карты
])
// Функция для переворота карты
const flipCard = (cardId) => {
  const cardIndex = cards.value.findIndex(card => card.id === cardId)
  if (cardIndex !== -1) {
    // Переключаем состояние
    cards.value[cardIndex].state =
        cards.value[cardIndex].state === 'closed' ? 'opened' : 'closed'

    // Здесь можно добавить логику проверки ответа
    // и обновить status карты
  }
}

// Обработчик для события flip из GameCard
const handleCardFlip = (cardId) => {
  flipCard(cardId)
}
</script>

<template>
  <Header :score="score"/>

  <div class="content">
    <GameCard
        :word="cards[0].word"
        :translation="cards[0].translation"
        :state="cards[0].state"
        :status="cards[0].status"
        @flip="() => handleCardFlip(cards[0].id)"
    />
    <main>
      <MainButton>Начать игру</MainButton>
    </main>
  </div>
</template>

<style scoped>
.content {
  padding-top: 120px;
  display: flex;
  flex: 1;
  gap: 120px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  margin-top: 120px;
}

</style>
