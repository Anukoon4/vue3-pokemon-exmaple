<template>
  <PokemonCard 
  :selectedId="selectedId" 
  :pokemons="starters"
   @pokemonClicked="fetchEvolution" />

  <PokemonCard :pokemons="evolutions" />
</template>

<script>
import Card from './card.vue'
import PokemonCard from './PokemonCard.vue'
const api = 'https://pokeapi.co/api/v2/pokemon'
const STARTER_ID = [1, 4, 7]
export default {
  components: {
    Card,
    PokemonCard,
  },
  data() {
    return {
      starters: [],
      evolutions: [],
      selectedId: null,
    }
  },
  async created() {
    const startData = await this.fetchData(STARTER_ID)
    this.starters = startData
  },

  methods: {
    async fetchEvolution(pokemon) {
      this.selectedId = pokemon.id
      const evolutions = await this.fetchData([pokemon.id + 1, pokemon.id + 2])
      this.evolutions = evolutions
    },
    async fetchData(ids) {
      const response = await Promise.all(
        ids.map((id) => window.fetch(api + '/' + id))
      )
      const data = await Promise.all(response.map((res) => res.json()))
      return data.map((dataElement) => {
        return {
          id: dataElement.id,
          name: dataElement.name,
          sprite: dataElement.sprites.other['official-artwork'].front_default,
          types: dataElement.types.map((type) => type.type.name),
        }
      })
    },
  },
}
</script>

<style scoped></style>
