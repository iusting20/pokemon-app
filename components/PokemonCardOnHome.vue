<template>
  <div>{{ pk_name }}</div>
</template>

<script>
export default {
  props: ["pk_name"],
};
</script>

<style lang="scss" scoped>
div {
  border: 3px solid blue;
  margin-top: 2em;
}
</style>
