<script setup>
import PokemonPage from './pages/PokemonPage.vue';

</script>

<template>
 

  <main class="container" >
    <PokemonPage />
  </main>
</template>

<style >
.container {
  max-width: 1280px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  padding: 2rem;

  font-weight: normal;
}

</style>
