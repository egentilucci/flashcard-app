<template>
  <q-card v-if="remainingCards.length !== 0">
    <q-card-section align="center">
      Card #{{ card.id }}
      {{ remainingCards }}
    </q-card-section>

    <q-separator inset />

    <q-card-section class="q-pt-none" align="center">
      {{ card.question }}
    </q-card-section>

    <q-separator inset />

    <q-card-section v-if="showAnswer" align="center">
      {{ card.answer }}
    </q-card-section>
    <q-card-section v-else align="center"> ? </q-card-section>

    <q-separator inset />

    <q-card-actions align="around">
      <q-btn flat @click="toggleAnswer" v-if="!showAnswer">SHOW</q-btn>
      <q-btn flat @click="toggleAnswer" v-else>HIDE</q-btn>
      <q-btn flat @click="nextCard">NEXT</q-btn>
    </q-card-actions>
  </q-card>
  <q-card v-else> NO MORE CARDS </q-card>
</template>

<script setup lang="ts">
import { defineProps, ref, computed } from 'vue';
import { Card } from '../components/models';

const props = defineProps<{
  deck: Array<Card>;
}>();

const showAnswer = ref(false);

const shuffleArray = (array: number[]) => {
  let shuffledArray = array.slice(); // Create a copy of the array
  for (let i = shuffledArray.length - 1; i > 0; i--) {
    // Generate a random index
    let j = Math.floor(Math.random() * (i + 1));
    // Swap elements at indices i and j
    [shuffledArray[i], shuffledArray[j]] = [shuffledArray[j], shuffledArray[i]];
  }
  return shuffledArray;
};

const remainingCards = ref(shuffleArray(props.deck.map((card) => card.id)));

const currentCardIndex = ref(0);

const card = computed(() => {
  return props.deck[remainingCards.value[currentCardIndex.value]];
});

const toggleAnswer = () => (showAnswer.value = !showAnswer.value);

const nextCard = () => {
  if (remainingCards.value.length !== 0) {
    remainingCards.value.splice(currentCardIndex.value, 1);
  }
};
</script>
