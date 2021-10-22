<template>
  <v-snackbar
      :value="openSnackbar"
      content-class="pa-0"
      absolute
      top
      :color="color"
  >
    <v-alert
        :type="color"
    >
      {{ text }}
    </v-alert>
    <template v-slot:action>
      <v-icon
          color="white"
          @click="$store.commit('closeSnackbar')"
      >
        mdi-close
      </v-icon>
    </template>
  </v-snackbar>
</template>

<script>
export default {
  props: {
    color: {
      type: String,
      required: true,
    },
    openSnackbar: {
      type: Boolean,
      required: true,
    },
    text: {
      type: String,
      required: true
    }
  },
}
</script>

<style lang="scss" scoped>
.v-alert {
  margin: 0;
}
</style>