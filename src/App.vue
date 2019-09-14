<template>
  <div id='q-app'>
    <router-view />
  </div>
</template>

<script>
import firebase from 'firebase'
import 'firebase/firestore'
import firebaseApp from 'firebase/app'
import Vuex from 'vuex'
import Vue from 'vue'
import { firestorePlugin } from 'vuefire'

var config = {
  apiKey: 'AIzaSyDg4fWlRe1EYzR0H_XkUUKvgBw82Z0rVAs',
  authDomain: 'storm-helper.firebaseapp.com',
  databaseURL: 'https://storm-helper.firebaseio.com',
  projectId: 'storm-helper',
  storageBucket: 'storm-helper.appspot.com',
  messagingSenderId: '1002502196572',
  appId: '1:1002502196572:web:d5f9e5a190431d04ac4599'
}

Vue.use(Vuex)
Vue.use(firestorePlugin)

const store = new Vuex.Store({
  state: {
    db: null,
    firebase: null,
    users: []
  },
  mutations: {
    addUser (state, user) {
      state.users.push(user)
    }
  }
})

export default {
  name: 'App',
  mounted () {
    firebase.initializeApp(config)
    store.state.db = firebase.firestore()
    store.state.firebase = firebaseApp
    console.log(this.$store)
  }
}
</script>

<style>
</style>
