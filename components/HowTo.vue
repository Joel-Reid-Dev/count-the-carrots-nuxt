<template>
  <div id="how-to-play">
    <h3>How to Play</h3>
    <p> Select Easy or Hard Mode. When you are ready to play, click "start the game". An alert will tell you
      what to count. Objects will start flying across the screen
      from both directions. You have to count the alerted item by clicking the count button for every
      requested item you see.</p>
    <p>When the animation is over and you are sure you are ready to check your score, click "Check
      Score" to see if you have won.
      <p>To Restart the game, simply click "Restart the Game"</p>
    </p>
    <GameSettings v-model="difficulty"/>
    <button @click="startGame">Start the Game!</button>
  </div>
</template>

<script setup lang="ts">

const difficulty = defineModel<string>('easy');

const emit = defineEmits<{
  (e:'play', difficulty:string): void
}>();

const startGame = () => {
  if (difficulty.value) {
    emit('play', difficulty.value)
  }
}



</script>

<style scoped lang="scss">
#how-to-play {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width:40rem;
  height:40rem;
  margin: 0 auto;
  background: #00dc82;
  color:black;
  padding:2rem;
  border-radius:0.25rem;
  text-align:center;
}
</style>