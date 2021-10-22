<template>
  <div class="d-flex justify-center">
    <v-form
        style="width:400px"
        ref="form"
        v-model="valid"
        lazy-validation
    >
      <v-text-field
          v-model="form.name"
          :rules="rules.name"
          label="Nome"
          required
      ></v-text-field>

      <v-text-field
          v-model="form.email"
          :rules="rules.email"
          label="E-mail"
          required
      ></v-text-field>

      <v-text-field
          v-model="form.contact"
          :rules="rules.contact"
          label="Telefone"
          required
          placeholder="(##) # ####-####"
          v-mask="'(##) # ####-####'"
      ></v-text-field>

      <v-file-input
          v-if="!contact"
          v-model="form.picture"
          :rules="rules.picture"
          show-size
          prepend-icon="mdi-camera"
          accept="image/*"
          label="Foto"
      ></v-file-input>

      <v-btn
          :loading="loading"
          :disabled="!valid || loading"
          color="success"
          class="mr-4"
          @click="newContact"
      >
        Salvar
      </v-btn>

      <v-btn
          :disabled="loading"
          color="error"
          class="mr-4"
          @click="reset"
      >
        Limpar Formulário
      </v-btn>
    </v-form>
  </div>
</template>

<script>
import {mask} from 'vue-the-mask'
export default {
  directives: {
    mask
  },
  props: {
    contact: {
      type: Object,
      default: () => {
      }
    }
  },
  data() {
    return {
      valid: true,
      form: {
        name: '',
        email: '',
        contact: '',
        picture: null
      },
      rules: {
        name: [
          v => !!v || 'Nome é obrigatório',
          v => (v && v.length >= 5) || 'O nome deve possuir no minímo 5 caracteres',
        ],
        email: [
          v => !!v || 'E-mail é obrigatório',
          v => /.+@.+\..+/.test(v) || 'E-mail inválido',
        ],
        contact: [
          v => !!v && v.length === 16 || 'Telefone é obrigatório',
        ],
        picture: [
          v => !!v || 'Foto é obrigatória',
          v => !v || v.size < 5000000 || 'O tamanho do arquivo deve ser inferior a 5Mb',
        ]
      }
    }
  },
  computed: {
    loading: {
      get() {
        return this.$store.state.loading
      },
      set(value) {
        this.$store.commit('setLoading', value)
      }
    }
  },
  watch: {
    contact: {
      handler(value) {
        this.form.name = value.name
        this.form.email = value.email
        this.form.contact = value.contact
      },
      deep: true
    }
  },
  methods: {
    async newContact() {
      await this.$refs.form.validate()
      if (!this.valid) {
        return
      }
      this.$store.commit('setLoading', true)
      const alert = {
        color: 'error',
        openSnackbar: true,
        text: 'O email informado já está cadastrado'
      }
      if (this.contact) {
        return this.$store.dispatch('updateContact', this.form)
            .then(() => {
              if(this.$store.state.status === 500) {
                this.$store.commit('setAlert', alert)
              } else {
                this.$router.push({name: 'Home'})
              }
            })
      }
      this.$store.dispatch('newContac', this.form)
          .then(() => {
            if(this.$store.state.status === 500) {
              this.$store.commit('setAlert', alert)
            } else {
              this.$router.push({name: 'Home'})
            }
          })
    },
    reset() {
      this.$refs.form.reset()
    },
  },
}
</script>

<style scoped>
</style>