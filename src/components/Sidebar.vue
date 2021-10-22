<template>
  <v-row justify="space-between" class="pa-3">
    <v-col class="text-h4">Contatos</v-col>
    <v-col>
      <v-row justify="end">
        <v-btn
            to="/contato"
            depressed
            color="primary"
        >
          Novo Contato
        </v-btn>
      </v-row>
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: "Sidebar"
}
</script>

<style scoped>
</style>