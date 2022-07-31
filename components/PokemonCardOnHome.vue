<template>
  <div>
    <v-card elevation="2" shaped>
      <v-card-title>
        {{ capitalizeFirstLetter(pk_name) }}
      </v-card-title></v-card
    >
    <br />
  </div>
</template>

<script>
export default {
  props: ["pk_name"],

  methods: {
    capitalizeFirstLetter(string) {
      return string.charAt(0).toUpperCase() + string.slice(1);
    },
  },
};
</script>

<style lang="scss" scoped>
v-card {
  margin-bottom: 50px;
}
</style>
