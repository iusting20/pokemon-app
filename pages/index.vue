<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <div v-for="pokemon in pokemonList.results">
        <PokemonCardOnHome :pk_name="pokemon.name"></PokemonCardOnHome>
      </div>
    </v-col>
  </v-row>
</template>

<script>
import PokemonCardOnHome from "~/components/PokemonCardOnHome.vue";
export default {
  name: "IndexPage",
  data() {
    return {
      pokemonList: "",
    };
  },
  async fetch() {
    this.pokemonList = await this.$axios.$get(
      "https://pokeapi.co/api/v2/pokemon/"
    );
  },
  components: { PokemonCardOnHome },
};
</script>
