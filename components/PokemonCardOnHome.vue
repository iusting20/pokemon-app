<template>
  <div>
    <v-card elevation="2" shaped>
      <v-row>
        <v-card-title>
          {{ capitalizeFirstLetter(pk_name) }}
        </v-card-title>
      </v-row>
      <v-row>
        <v-col cols="6" sm="6" md="6">
          <v-card-text>
            Types:
            <li v-for="type in pokemonProfileInfo.types">
              {{ type.type.name }}
            </li>
          </v-card-text>
        </v-col>
        <v-col cols="6" sm="6" md="6">
          <img :src="pokemonAvatar" />
        </v-col>
      </v-row>
    </v-card>
  </div>
</template>

<script>
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
};
</script>

<style lang="scss" scoped>
v-card {
  margin-bottom: 50px;
}
</style>
