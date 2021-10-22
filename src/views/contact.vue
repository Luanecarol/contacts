<template>
  <div>
    <top />
    <form-contact/>
    <alert-top-right :color="alert.color" :open-snackbar="alert.openSnackbar" :text="alert.text"/>
  </div>
</template>

<script>
import FormContact from "../components/FormContact";
import AlertTopRight from "../components/AlertTopRight";
import Top from "../components/Top";
export default {
  components: {
    Top,
    AlertTopRight,
    FormContact,
  },
  computed: {
    alert() {
      return this.$store.state.alert
    }
  }
}
</script>