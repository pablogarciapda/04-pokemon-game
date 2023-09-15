<script setup>
defineProps({
  pokemons: {
    type: Array,
    required: true,
  },
  bloqueo: {
    type: Boolean,
  },
})
</script>

<template>
  <div class="option-container">
    <ul>
      <li
        v-for="pokemon in pokemons"
        :key="pokemon.id"
        @click="$emit('selection-pokemon', pokemon.id)"
        disabled="true"
      >
        <button
          class="boton"
          @click="$emit('selection-pokemon', pokemon.id)"
          :disabled="bloqueo"
        >
          {{ pokemon.name }}
        </button>
      </li>
    </ul>
  </div>
</template>

<style scoped>
/* Pokemon Options */
ul {
  list-style-type: none;
}
li {
  background-color: white;
  border-radius: 5px;
  border: 1px solid rgba(0, 0, 0, 0.2);
  cursor: pointer;
  margin-bottom: 10px;
  width: 250px;
  padding: 10px;
  text-align: center;
}

li:hover {
  background-color: rgba(0, 0, 0, 0.05);
}

.options-container {
  display: flex;
  justify-content: center;
}
.boton {
  width: 100%;
  height: 100%;
}
</style>
