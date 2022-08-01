<template>
  <div>
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
    <v-row justify="center" align="center">
      <a :href="prevPageApiUrl">
        <v-btn
          :disabled="!!!prevPageApiUrl"
          elevation="3"
          color="primary"
          class="prevNextButton"
          >&lt PREV</v-btn
        >
      </a>
      <a :href="nextPageApiUrl">
        <v-btn
          :disabled="!!!nextPageApiUrl"
          elevation="3"
          color="primary"
          class="prevNextButton"
          >NEXT &gt</v-btn
        >
      </a>
    </v-row>
    <br />
    <br />
  </div>
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
      nextPageApiUrl: "",
      prevPageApiUrl: "",
      offset: 0,
    };
  },
  async fetch() {
    if (this.$route.query.offset) {
      this.offset = this.$route.query.offset;
    }

    this.pokemonData = await this.$axios.$get(
      "https://pokeapi.co/api/v2/pokemon/?offset=" + this.offset + "&limit=20"
    );

    // CONSTRUCTING BUTTON LINKS
    if (this.pokemonData.previous != null) {
      let linkPcsPrev = this.pokemonData.previous.split(
        "https://pokeapi.co/api/v2/pokemon/"
      );
      this.prevPageApiUrl = "/" + linkPcsPrev[1];
    }
    //
    // CONSTRUCTING BUTTON LINKS
    if (this.pokemonData.next != null) {
      let linkPcsNext = this.pokemonData.next.split(
        "https://pokeapi.co/api/v2/pokemon/"
      );
      this.nextPageApiUrl = "/" + linkPcsNext[1];
    }
  },
  components: { PokemonCardOnHome, AppTitle },
};
</script>

<style scoped>
.prevNextButton {
  margin-left: 10em;
  margin-right: 10em;
}

a {
  text-decoration: none;
}
</style>
