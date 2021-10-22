<template>
  <div>
    <top />
    <form-contact :contact="$store.state.contact"/>
    <loading/>
  </div>
</template>

<script>
import FormContact from "../components/FormContact";
import Loading from "../components/Loading";
import Top from "../components/Top";
export default {
  components: {
    Top,
    Loading,
    FormContact
  },
  mounted() {
    const {id} = this.$route.params
    this.$store.dispatch('getContactByID', id)
  }
}
</script>

<style scoped>
</style>