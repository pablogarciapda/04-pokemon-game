<script setup>
import { computed } from 'vue'

const props = defineProps({
  pokemonId: {
    type: Number,
    required: true,
  },
  showPokemon: {
    type: Boolean,
    required: true,
    default: false,
  },
})
const urlPokemon = computed(
  () =>
    `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${props.pokemonId}.svg`
)
</script>

<template>
  <div class="pokemon-container">
    <img class="hidden-pokemon" :src="urlPokemon" alt="pokemon " />
    <img v-if="showPokemon" class="fade-in" :src="urlPokemon" alt="pokemon " />
  </div>
</template>

<style scoped>
/* Pokemon Picture */
.pokemon-container {
  height: 200px;
}

img {
  height: 200px;
  position: absolute;
  right: 32%;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}

.hidden-pokemon {
  filter: brightness(0);
}
</style>
