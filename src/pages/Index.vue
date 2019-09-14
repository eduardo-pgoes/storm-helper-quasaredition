<template>
  <q-page class="flex flex-center">
    <img alt="Quasar logo" src="~assets/quasar-logo-full.svg">
  </q-page>
</template>

<style>
</style>

<script>
import firebase from 'firebase'
export default {
  name: 'PageIndex',
  mounted () {
    if (!firebase.auth().currentUser) {
      this.$router.push('login')
    }
  }
}
</script>
