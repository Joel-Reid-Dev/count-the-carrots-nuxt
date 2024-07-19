<template>
  <h1>
    <slot />
  </h1>
</template>

<script setup lang="ts">

</script>

<style scoped lang="scss">
  h1 {
    background: -webkit-linear-gradient(red,orange,purple,red);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    display:flex;
    justify-content: center;
    font-size:4rem;
  }
</style>