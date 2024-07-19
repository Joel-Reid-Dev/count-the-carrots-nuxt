<template>
  <fieldset>
    <legend>Difficulty:</legend>
    <div>
      <input type="radio" id="easy" name="difficulty" value="easy" v-model="model" @change="updateDifficulty" />
      <label for="easy">Easy</label>

      <input type="radio" id="hard" name="difficulty" value="hard" v-model="model" @change="updateDifficulty" />
      <label for="hard">Hard</label>
    </div>
  </fieldset>
</template>

<script setup lang="ts">
const model = defineModel<string>('easy');
const emit = defineEmits<{
  (e:'update:modelValue', difficulty:string): void
}>();

const updateDifficulty = () => {
  if (model.value) {
    emit('update:modelValue', model.value);
  }
}

</script>

<style scoped lang="scss">

</style>