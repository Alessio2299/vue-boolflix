<template>
  <div id="app">
    <HeaderPage />
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
      loading: true
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
      for(let i = 6; i < 12; i++){
      this.popularFilms.push(response.data.results[i]) 
      }
    })
    axios.get('https://api.themoviedb.org/3/tv/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT')
    .then(response => {
      console.log(response)
      for(let i = 0; i < 6; i++){
      this.popularTv.push(response.data.results[i]) 
      }
    })
  },
  methods:{      
  }
}
</script>

<style lang="scss">
  @import "./assets/style/general.scss";
  @import '~@fortawesome/fontawesome-free/css/all.css';
</style>
