<template>
  <div>
    <v-row>
      <v-col class="text-center">
        <AppTitle></AppTitle>
        <a href="/">
          <v-btn elevation="3" color="secondary" class="prevNextButton"
            >&lt BACK
          </v-btn>
        </a>
        <br />
        <br />
        <br />
        <h1>{{ capitalizeFirstLetter(pk_name) }}</h1>
      </v-col>
    </v-row>

    <v-row>
      <v-col class="text-center">
        <img :src="pokemonAvatar" alt="" />
      </v-col>
    </v-row>

    <v-row>
      <v-col class="text-center">
        <h2>INFO</h2>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: "Profile",
  data() {
    return {
      pokemonId: this.$route.query.pokemonId,
      pk_name: "",
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
    this.pokemonProfileInfo = await this.$axios.$get(
      "https://pokeapi.co/api/v2/pokemon/" + this.pokemonId
    );
    this.pokemonAvatar = this.pokemonProfileInfo.sprites.front_default;
    this.pk_name = this.pokemonProfileInfo.name;
  },
};
</script>

<style scoped>
a {
  text-decoration: none;
}
</style>
