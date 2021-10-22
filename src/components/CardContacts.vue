<template>
  <div>
    <v-row>
      <v-card width="400" class="ma-5" v-for="contact in contacts" :key="contact.id">
        <v-card-title class="mt-8">
          <v-avatar size="80">
            <img
                alt="user"
                :src="`${baseUrl}/${contact.picture}`"
            >
          </v-avatar>
          <div class="ml-3 d-flex flex-column">
            <p class="ma-0">
              {{ contact.name }}
            </p>
            <span class="text-subtitle-1">{{ contact.email }}</span>
            <span class="text-subtitle-1">{{ contact.contact }}</span>
          </div>
        </v-card-title>
        <v-card-actions>
          <v-btn
              @click="deleteContact(contact)"
              dark
              color="red lighten-2"
          >
            <v-icon
                left
                dark
            >
              mdi-delete
            </v-icon>
            Excluir
          </v-btn>
          <v-btn
              :to="`/contato/${contact.id}`"
              dark
              color="green lighten-2"
          >
            <v-icon
                left
                dark
            >
              mdi-pencil
            </v-icon>
            Editar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return 
  },
  computed: {
    contacts() {
      return this.$store.state.contacts
    }
  },
  mounted() {
    this.$store.dispatch('getContacts')
  },
  methods: {
    deleteContact(contac) {
      this.$store.commit('setDialog')
      this.$store.commit('setContact', contac)
    }
  }
}
</script>

<style scoped>
</style>