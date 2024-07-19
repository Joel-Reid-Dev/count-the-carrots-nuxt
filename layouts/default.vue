<template>
  <div class="container">
    <Navbar/>
    <slot/>
  </div>
</template>

<script setup lang="ts">

</script>

<style scoped lang="scss">

.container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: black;
  color:white;
}
</style>