<template>
  <div>
    <v-card elevation="2" shaped>
      <v-row>
        <v-card-title>
          {{ capitalizeFirstLetter(pk_name) }}
        </v-card-title>
      </v-row>

      <v-row>
        <v-col cols="4" sm="4" md="4">
          <img :src="pokemonAvatar" />
        </v-col>

        <PokemonCardOnHomeType
          :pokemonProfileInfo="pokemonProfileInfo"
        ></PokemonCardOnHomeType>

        <v-col cols="4" sm="4" md="4">
          <a :href="'/profile?pokemonId=' + pokemonProfileInfo.id"
            ><v-btn elevation="3">MORE</v-btn></a
          >
        </v-col>
      </v-row>
    </v-card>
    <br />
    <br />
  </div>
</template>

<script>
import PokemonCardOnHomeType from "./pokemonCardOnHomeType.vue";
export default {
  props: ["pk_name", "pk_url"],
  data() {
    return {
      pokemonProfileInfo: "",
      pokemonAvatar: "",
    };
  },
  methods: {
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
  },
  async fetch() {
    this.pokemonProfileInfo = await this.$axios.$get(this.pk_url);
    this.pokemonAvatar = this.pokemonProfileInfo.sprites.front_default;
  },
  components: { PokemonCardOnHomeType },
};
</script>

<style lang="scss" scoped>
a {
  text-decoration: none;
}
</style>
