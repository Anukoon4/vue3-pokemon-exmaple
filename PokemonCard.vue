<template>
  <div class="cards ">
    <card
      v-for="starter in pokemons"
      @click="click(starter)"
      :class="{ opace: selectedId && starter.id !== selectedId }"
    >
      <template v-slot:title> {{ starter.name }} # {{ starter.id }} </template>
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
export default {
  components: {
    Card,
  },
  props: {
    pokemons: {
      type: Array,
    },
    selectedId:{
        type:Number
    }
  },
  methods:{
    click(pokemon){
        this.$emit("pokemonClicked",pokemon)
    }
  }
}
</script>

<style scoped>
.cards {
  display: flex;
}
.opace{
  opacity: 0.5;
}
.card:hover{
  opacity: 1.0;
}
img {
  width: 100%;
}</style>
