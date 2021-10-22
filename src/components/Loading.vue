<template>
  <v-overlay :value="$store.state.overlay">
    <v-progress-circular
        indeterminate
        size="64"
    ></v-progress-circular>
  </v-overlay>
</template>

<script>
export default {
  name: "Loading"
}
</script>

<style scoped>
</style>