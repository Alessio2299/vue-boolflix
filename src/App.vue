<template>
  <div id="app">
    <HeaderPage />
    <MainPage :listPopularFilms="popularFilms"/>
  </div>
</template>

<script>
 import HeaderPage from "./components/HeaderPage.vue"
 import MainPage from "./components/MainPage.vue"
export default {
  name: 'App',
  data(){
    return{
      popularFilms: []
    }
  },
  components: {
    HeaderPage,
    MainPage
  },
  mounted(){
    const axios = require('axios');
    axios.get('https://api.themoviedb.org/3/movie/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT')
    .then(response => {this.popularFilms = response.data.results})      
  },
  methods:{      
  }
}
</script>

<style lang="scss">
  @import "./assets/style/general.scss";
  @import '~@fortawesome/fontawesome-free/css/all.css';
</style>
