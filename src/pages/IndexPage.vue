<template>
  <q-page class="row items-center justify-evenly">
    <QuestionsDeck :deck="deck"></QuestionsDeck>
  </q-page>
</template>

<script setup lang="ts">
import QuestionsDeck from '../components/QuestionsDeck.vue';
import SDprinciplesDeck from '../assets/data/software_development_principles.json';

const deck = SDprinciplesDeck;
</script>
