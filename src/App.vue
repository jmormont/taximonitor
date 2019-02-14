<template>
  <v-app>
     <v-navigation-drawer
      v-model="drawer"
      fixed
      app
    >
      <v-list dense>
        <v-list-tile @click="">
          <v-list-tile-action>
            <v-icon>home</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>Home</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile @click="">
          <v-list-tile-action>
            <v-icon>contact_mail</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title>Contact</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar app>
      <v-toolbar-side-icon @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="headline text-uppercase">
        <span >Монитор</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <auth-btn></auth-btn>
    </v-toolbar>

    <v-content>
      <HelloWorld/>
    </v-content>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'
import AuthBtn from './components/AuthBtn'

export default {
  name: 'App',
  components: {
    HelloWorld, AuthBtn
  },
  data () {
    return {
      drawer: null
    }
  },
  mounted() {
    var config = {
      apiKey: "AIzaSyBoN5S0L48In_peNTm5x1RkShK1n_MBsb8",
      authDomain: "yandextaxi.firebaseapp.com",
      databaseURL: "https://yandextaxi.firebaseio.com",
      projectId: "yandextaxi",
      storageBucket: "yandextaxi.appspot.com",
      messagingSenderId: "208720131553"
    }
    firebase.initializeApp(config)
    window.firebase = firebase
    window.db = firebase.firestore
  }
}
</script>
