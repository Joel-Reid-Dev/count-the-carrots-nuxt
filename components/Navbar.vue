<template>
  <nav>
    <ul>
      <li v-if="route.name == 'index'">
        <NuxtLink to="/admin">Admin</NuxtLink>
      </li>
      <li v-if="route.name == 'admin'">
        <NuxtLink to="/">Home</NuxtLink>
      </li>
    </ul>
  </nav>
</template>

<script setup lang="ts">
const route = useRoute();

</script>

<style scoped lang="scss">
  ul {
    position:absolute;
    right:5rem;
  }
</style>