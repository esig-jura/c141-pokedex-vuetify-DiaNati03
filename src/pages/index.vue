<template>
  <v-container>
    <h1 class="mb-6 text-center">Pokédex</h1>

    <v-text-field
      v-model="search"
      clearable
      label="Rechercher un Pokémon"
      prepend-icon="mdi-magnify"
    />

    <v-row>
      <!-- Exemple de colonne vide (à dupliquer plus tard avec du contenu) -->
      <v-col
        v-for="pokemon in filteredPokemons"
        :key="pokemon.id"
        cols="12"
        lg="3"
        md="4"
        sm="6"
        xl="2"
        xs="12"
      >
        <PokemonCard :pokemon="pokemon" />
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
// Importer le magasin des pokémons
// @/ => représente le dossier src
  import { usePokemonStore } from '@/stores/pokemonStore'
  import PokemonCard from '@/components/PokemonCard.vue'
  import { computed, ref } from 'vue'

  // Récupère le magasin des Pokémon
  const pokemonStore = usePokemonStore()
  const search = ref('')
  const filteredPokemons = computed(() => {
    const query = search.value.toLowerCase().trim()
    return sortedPokemons.value.filter(pokemon =>
      pokemon.name.toLowerCase().includes(query)
    )
  })
  const sortedPokemons = computed(() => {
    return [...pokemonStore.pokemons].sort((a, b) =>
      a.name.localeCompare(b.name)
    )
  })
</script>

<style scoped>
/* Animation pour l'icône de favori */
:deep(.mdi-heart) {
  animation: heartbeat 1s ease-in-out;
}
</style>
