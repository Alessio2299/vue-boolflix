<template>
  <div id="app">
    <HeaderPage @textSearch="search"/>
    <MainPage :listPopularFilms="popularFilms" :listPopularTv="popularTv"/>
  </div>
</template>

<script>
 import HeaderPage from "./components/HeaderPage.vue"
 import MainPage from "./components/MainPage.vue"
export default {
  name: 'App',
  data(){
    return{
      popularFilms: [],
      popularTv: [],
      loading: true,
      searchText: ""
    }
  },
  components: {
    HeaderPage,
    MainPage
  },
  mounted(){
    const axios = require('axios');
    axios.get('https://api.themoviedb.org/3/movie/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT')
    .then(response => {
      console.log(response)
      this.popularFilms = response.data.results
    })
    axios.get('https://api.themoviedb.org/3/tv/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT')
    .then(response => {
      console.log(response)
      this.popularTv = response.data.results
    })
  },
  methods:{    
    search(value){
      this.searchText = value
    }  
  }
}
</script>

<style lang="scss">
  @import "./assets/style/general.scss";
  @import '~@fortawesome/fontawesome-free/css/all.css';
</style>
