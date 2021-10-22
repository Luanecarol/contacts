<template>
  <v-row justify="center">
    <v-dialog
        v-model="dialog"
        persistent
        max-width="400"
    >
      <v-card>
        <v-card-title class="text-h5">
          Confirma a exclusão do
          <hr>
          contato?
        </v-card-title>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn
              :disabled="$store.state.loading"
              color="error"
              @click="$store.commit('setDialog')"
          >
            Cancelar
          </v-btn>
          <v-btn
              :disabled="$store.state.loading"
              :loading="$store.state.loading"
              color="primary"
              @click="deteleContact"
          >
            Confirmar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  computed: {
    dialog: {
      get() {
        return this.$store.state.dialog
      },
      set(value) {
        this.$store.commit('setLoading', value)
      }
    }
  },
  methods: {
    deteleContact() {
      this.$store.commit('setLoading', true)
      this.$store.dispatch('deleteContactById')
    }
  }
}
</script>

<style scoped>
</style>