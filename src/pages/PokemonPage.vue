<script setup>
import { computed, onMounted, ref } from 'vue'
import PokemonOption from '../components/PokemonOption.vue'
import PokemonPicture from '../components/PokemonPicture.vue'
import getPokemonOptions from '../helpers/pokemonOptions.js'

const pokemonArr = ref([])
const pokemon = ref(null)
const showPokemon = false

onMounted(async () => {
  pokemonArr.value = await getPokemonOptions()

  const rndInt = Math.floor(Math.random() * 4)
  pokemon.value = pokemonArr.value[rndInt]
})
</script>

<template>
  <h1 v-if="!pokemon">Espere porfavor ....</h1>
  <div v-else>
    <h1>Que pokemon es</h1>
    <!-- todo imagen pokemon -->
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <!-- todo Opciones pokemon -->
    <PokemonOption :pokemons="pokemonArr" />
  </div>
</template>

<style scoped></style>
