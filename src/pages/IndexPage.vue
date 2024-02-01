<template>
  <q-page class="column items-center">
    <q-tabs v-model="tab" class="q-pa-md">
      <q-tab v-for="tab in tabs" :key="tab" :name="tab" :label="tab" />
    </q-tabs>
    <QuestionsDeck :deck="deck" :key="tab"></QuestionsDeck>
  </q-page>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import QuestionsDeck from '../components/QuestionsDeck.vue';
import principles from '../assets/data/software_development_principles.json';
import typescript from '../assets/data/typescript.json';

const decks = { principles, typescript };
const tabs = Object.keys(decks);

const deck = computed(() => {
  return decks[tab.value];
});

const tab = ref(tabs[0] as keyof typeof decks);
</script>
