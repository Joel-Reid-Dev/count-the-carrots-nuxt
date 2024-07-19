<template>
  <CarrotHeader>
    Count The Carrots
  </CarrotHeader>
  <HowTo
      v-if="!startGame"
      @play="playGame"
  />
  <div v-if="(selectedDifficulty =='hard' && startGame)">
    <HardGameWarning/>
  </div>
</template>

<script setup lang="ts">
const startGame = ref(false);
const selectedDifficulty = ref('');

const playGame = (difficulty) => {
  startGame.value = true;
  selectedDifficulty.value = difficulty;
}
</script>

