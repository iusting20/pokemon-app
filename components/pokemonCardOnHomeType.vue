<template>
  <v-col cols="4" sm="4" md="4">
    <v-card-text>
      <h3>Types:</h3>
      <li v-for="type in pokemonProfileInfo.types">
        {{ type.type.name }}
      </li>
    </v-card-text>
  </v-col>
</template>

<script>
export default {
  props: ["pokemonProfileInfo"],
};
</script>

<style lang="scss" scoped></style>
