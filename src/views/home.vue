<template>
  <div>
    <sidebar/>
    <card-contacts/>
    <dialog-delete/>
    <alert-top-center :color="alert.color" :open-snackbar="alert.openSnackbar" :text="alert.text"/>
    <loading/>
  </div>
</template>

<script>
import CardContacts from '../components/CardContacts'
import Sidebar from "../components/Sidebar";
import DialogDelete from "../components/DialogDelete";
import AlertTopCenter from "../components/AlertTopCenter";
import Loading from "../components/Loading";
export default {
  components: {
    Loading,
    AlertTopCenter,
    DialogDelete,
    Sidebar,
    CardContacts,
  },
  computed: {
    alert() {
      return this.$store.state.alert
    }
  }
}
</script>