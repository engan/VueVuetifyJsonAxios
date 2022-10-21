<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <router-link to="/">Home</router-link>&nbsp;|&nbsp;<router-link to="/about">About</router-link>&nbsp;|&nbsp;<router-link to="/cards">Cards</router-link>
      <v-spacer></v-spacer>
      <v-btn
        flat
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
      >
        <span class="mr-2">Latest Release</span>
      </v-btn>
    </v-toolbar>

    <v-content>
      <router-view/>
    </v-content>
  </v-app>
  
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data () {
    return {
      Items: [],
    }
  },
  methods: {
    async getItem() {
      await axios.get('../data/data.json') 
      .then((response) => {
        this.Items = response.data;
         response.status == 200 && response.data.length > 0 

         // sessionStorage is used to store JSON data so that the file data.json 
         // does not need to be loaded for each component in which it is used
         ? sessionStorage.setItem("JSONdata", JSON.stringify(this.Items)) 
         : sessionStorage.removeItem("JSONdata")
      })
    }
  },
  created() {
    this.getItem()
  }
}
</script>
