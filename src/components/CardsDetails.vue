<template>
  <v-container>
    <v-card-title primary-title class="justify-center" v-for="item in filteredItems" :key="item.id">
      <div class="cards white--text">
        <h3 class="headline white--text text--accent-2" style="">{{item.title}}</h3>
        <div style="padding-bottom: 20px">{{item.long}}</div>
      </div>
    </v-card-title>
  </v-container>
</template>

<script>
export default {
  name: 'app',
  data: function() { 
      return {
        Items: []
      }
  },
  // async mounted() {
  //   await this.$http.get('../data/data.json')
  //     .then(response => {

  //     // Filter the result directly from the API, BEFORE returning full result   
  //     this.Items = response.data.filter(item => item.id == this.$route.params.id)

  //     // Use this instead if computed: filteredItems() below is used:
  //     this.Items = response.data
  //     // filteredItems() filters the result AFTER the API is returning full result
  //   })
  // },

  // Used if the result should be filtered AFTER the API is returning full result
  // Use v-for="item in filteredItems" instead of v-for="item in Items" in <v-card-title
  computed: { 
    filteredItems(){
        return this.Items.filter(item => item.id == this.$route.params.id)
    }
  },
  created() {
    // Used instead of mounted() above. Load data.json only once pr session 
    this.Items = JSON.parse(sessionStorage.getItem('JSONdata'))
  }
}
</script>

<style lang="scss">
  h3 {
    padding-bottom: 10px
  }  
  .cards {
    border: #aaa 1px solid; 
    border-radius: 3px; 
    width: 50%; 
    background-color:#00796a; 
    padding: 10px 15px 0 15px;
    font-weight: lighter;  
  }
</style>
