<template>
  <div class="cards">
    <card v-for="starter in starters">
      <template v-slot:title>
        {{ starter.name }}
      </template>
      <template v-slot:image>
        <img :src="starter.sprite" />
      </template>

      <template v-slot:description>
        <div v-for="type in starter.types">
          {{ type }}
        </div>
      </template>
    </card>
  </div>
</template>

<script>
import Card from './card.vue'
const api = 'https://pokeapi.co/api/v2/pokemon'
const ids = [1, 4, 7]
export default {
  components: {
    Card,
  },
  data() {
    return {
      starters: [],
    }
  },
  created() {
    this.fetchData()
  },

  methods: {
    async fetchData() {
      const response = await Promise.all(
        ids.map((id) => window.fetch(api + '/' + id))
      )
      const data = await Promise.all(response.map((res) => res.json()))
      this.starters = data.map((dataElement) => {
        return {
          name: dataElement.name,
          sprite: dataElement.sprites.other['official-artwork'].front_default,
          types: dataElement.types.map((type) => type.type.name),
        }
      })
    },
  },
}
</script>

<style scoped>
.cards {
  display: flex;
}
img {
  width: 100%;
}
</style>
