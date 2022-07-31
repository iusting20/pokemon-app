<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="8" md="6">
      <AppTitle></AppTitle>

      <div v-for="pokemon in pokemonData.results">
        <PokemonCardOnHome
          :pk_name="pokemon.name"
          :pk_url="pokemon.url"
        ></PokemonCardOnHome>
      </div>
    </v-col>
  </v-row>
</template>

<script>
import PokemonCardOnHome from "~/components/PokemonCardOnHome.vue";
import AppTitle from "../components/AppTitle.vue";
export default {
  name: "IndexPage",
  data() {
    return {
      pokemonData: "",
      pokemons: [],
    };
  },
  async fetch() {
    this.pokemonData = await this.$axios.$get(
      "https://pokeapi.co/api/v2/pokemon/"
    );
  },
  components: { PokemonCardOnHome, AppTitle },
};
</script>
