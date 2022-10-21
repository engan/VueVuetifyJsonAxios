<template>
    <v-container>

      <v-card-title class="justify-center search-wrapper">
        <input type="text" class="white--text " style="width: 50%; height: 30px" v-model="keyword" placeholder="Search in title or text" />
      </v-card-title>

      <v-card-title primary-title class="justify-center" v-for="item in filteredList" :key="item.id">
      <div class="cards white--text">
        <h3 class="headline white--text text--accent-2" style="">{{item.title}}</h3>
        <div style="padding-bottom: 10px">{{item.short}}</div>
          <v-card-actions class="justify-left" style="padding-left: 0">
            <router-link :to="`/card/${item.id}`" class="white--text">SEE MORE</router-link>
          </v-card-actions>
        </div>
      </v-card-title>

  </v-container>
</template>

<script>
export default {
  name: 'app',
  data: function() { 
      return {
        keyword: '',
        Items: []
      }
  },
  computed: {
    filteredList() {
      return this.Items.filter((item) => {
        return item.title.toLowerCase().includes(this.keyword.toLowerCase()) 
            || item.short.toLowerCase().includes(this.keyword.toLowerCase());
      });
    }
  },

  // // Alternative: methods: getItem() and created() this.getItem() 
  // // (data.json file loaded more than once)
  // methods: {
  //   async getItem() {
  //     await this.$http.get('data/data.json')
  //     .then((response) => {
  //       this.Items = response.data;
  //     })
  //   }
  // },

  created() {
    // this.getItem()
    
    // Used instead of methods: getItem() and created() above.
    // data.json loaded only once in App.vue. Sessions on all other components
    this.Items = JSON.parse(sessionStorage.getItem('JSONdata'))
  }
}
</script>

<style lang="scss">
::placeholder {
  color: #ddd;
  padding: 10px 15px 0 5px
}
input {
  border-radius: 3px; 
  border: 1px #ccc solid;
  background-color:#00796a; 
  font-weight: lighter;
}
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
