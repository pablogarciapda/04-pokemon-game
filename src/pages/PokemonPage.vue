<script setup>
import { computed, onMounted, ref } from 'vue'
import PokemonOption from '../components/PokemonOption.vue'
import PokemonPicture from '../components/PokemonPicture.vue'
import getPokemonOptions from '../helpers/pokemonOptions.js'

const pokemonArr = ref([])
const pokemon = ref(null)
const showPokemon = ref(false)
const showAnswer = ref(false)
const message = ref('')
const bloqueo = ref(false)

const selection = pokemonId => {
  showPokemon.value = true
  showAnswer.value = true
  if (pokemon.value.id == pokemonId) {
    message.value = 'has acertado el Pokemon'
  } else {
    message.value = ' Fallaste ... '
    bloqueo.value = true
    setTimeout(() => {
      message.value = ''
      bloqueo.value = false
      showPokemon.value = false
      iniciarJuego()
    }, 3000)
  }
}

onMounted(() => {
  iniciarJuego()
})

const iniciarJuego = async () => {
  pokemonArr.value = await getPokemonOptions()

  const rndInt = Math.floor(Math.random() * 4)
  pokemon.value = pokemonArr.value[rndInt]
  message.value = ''
  bloqueo.value = false
  showPokemon.value = false
  showAnswer.value = false
}
</script>

<template>
  <h1 v-if="!pokemon">Espere porfavor ....</h1>
  <div v-else class="container">
    <h1>PELAYO</h1>
    <img class="mini" src="../assets/IMG_20230915_203733.jpg" alt="pelayo" />
    <h1>Que pokemon es</h1>
    <!-- todo imagen pokemon -->
    <PokemonPicture :pokemonId="pokemon.id" :showPokemon="showPokemon" />
    <!-- todo Opciones pokemon -->
    <PokemonOption
      :pokemons="pokemonArr"
      :bloqueo="bloqueo"
      @selection-pokemon="selection"
    />
    <template v-if="showAnswer">
      <h2>{{ message }}</h2>
      <button>nuevo juego</button>
    </template>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  justify-content: center;
}
.mini {
  margin: 0;
  height: 100px;
  position: center;
  user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  -webkit-user-drag: none;
  -webkit-user-select: none;
}
h1 {
  margin: 0;
}
</style>
