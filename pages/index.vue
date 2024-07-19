<template>
  <CarrotHeader>
    Count The Pokemon
  </CarrotHeader>
  <HowTo
      v-if="!startGame"
      @play="playGame"
  />
  <div v-if="(selectedDifficulty =='hard' && startGame)">
    <HardGameWarning/>
  </div>
  <GameCanvas
      v-if="startGame"
      :difficulty="selectedDifficulty"
      />
</template>

<script setup lang="ts">
const startGame = ref(false);
const selectedDifficulty = ref('');

const playGame = (difficulty:string) => {
  startGame.value = true;
  selectedDifficulty.value = difficulty;
}
</script>

