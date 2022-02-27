<template>
  <div id="app">
    <HeaderPage @textSearch="search"/>
    <MainPage :listFilm="film" :listTv="seriesTv" />
  </div>
</template>

<script>
 import HeaderPage from "./components/HeaderPage.vue"
 import MainPage from "./components/MainPage.vue" 
export default {
  name: 'App',
  data(){
    return{
      film: [],
      seriesTv: [],
      loading: true,
      searchText: "",
      urlFilm: `https://api.themoviedb.org/3/movie/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`,
      urlSeries: `https://api.themoviedb.org/3/tv/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`
    }
  },
  components: {
    HeaderPage,
    MainPage
  },
  watch: {
    urlFilm(newValue){
      this.getSeriesFilm(newValue, "film")
      console.log(newValue)
    },
    urlSeries(newValue){
      this.getSeriesFilm(newValue, "seriesTv")
      console.log(newValue)
    }
  },
  mounted(){
    this.getSeriesFilm(this.urlFilm, "film");
    this.getSeriesFilm(this.urlSeries, "seriesTv")
  },
  methods:{    
    search(value){
      this.searchText = value
      this.urlFilm = `https://api.themoviedb.org/3/search/movie?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT&query=${value}`;
      this.urlSeries = `https://api.themoviedb.org/3/search/tv?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT&query=${value}`;
      if(this.searchText == ""){
        this.urlFilm = `https://api.themoviedb.org/3/movie/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`;
        this.urlSeries = `https://api.themoviedb.org/3/tv/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`;
        
      }
    },
    getSeriesFilm(API, array){
      const axios = require('axios')
      axios.get(API)
      .then(response => {
        this[array] = response.data.results
      })
    }
  }
}
</script>

<style lang="scss">
  @import "./assets/style/general.scss";
  @import '~@fortawesome/fontawesome-free/css/all.css';
</style>
