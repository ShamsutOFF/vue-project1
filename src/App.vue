<script setup>
import {onMounted, ref} from 'vue'
import MainButton from "@/components/MainButton.vue";
import Header from "@/components/Header.vue";
import GameCard from "@/components/GameCard.vue";

const API_URL = 'http://localhost:8080/api/random-words'

function getRandomWords() {
  return fetch(API_URL)
      .then(response => response.json())
}

let cardId = 1;

onMounted(() => {
  getRandomWords()
      .then(words => {
        cards.value = words.map((word, index) => ({
          id: cardId++,
          word: word.word,
          translation: word.translation,
          state: 'closed',
          status: 'default',
          number: (index + 1).toString().padStart(2, '0')
        }))
      })
})

const cards = ref([]);

const handleFlip = (cardId) => {
  const card = cards.value.find(c => c.id === cardId)
  if (card && card.status === 'default') {
    card.status = 'flipped'
  }
}

const handleAnswer = (cardId, isCorrect) => {
  const card = cards.value.find(c => c.id === cardId)
  if (card && card.status === 'flipped') {
    card.status = isCorrect ? 'correct' : 'incorrect'
  }
}
</script>

<template>
  <Header/>
  <div class="content">
    <div class="cards-container">
      <GameCard
          v-for="card in cards"
          :key="card.id"
          :card="card"
          @flip="handleFlip"
          @answer="handleAnswer"
      />
    </div>
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

.cards-container {
  display: flex;
  gap: 20px;
  flex-wrap: wrap;
  justify-content: center;
}
</style>
