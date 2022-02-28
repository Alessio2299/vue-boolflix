<template>
  <div id="app">
    <HeaderPage @textSearch="search"/>
    <MainPage @valueSliderFilm="newValueSlider" :listFilm="film" :listTv="seriesTv" :value="value"/>
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
      urlSeries: `https://api.themoviedb.org/3/tv/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`,
      // Valori Slider, che servono per il ciclo for
      nextFilm: 6,
      prevFilm: 0,
      value: 1,
    }
  },
  components: {
    HeaderPage,
    MainPage
  },
  watch: {
    urlFilm(newValue){
      this.getSeriesFilm(newValue, "film")
    },
    urlSeries(newValue){
      this.getSeriesFilm(newValue, "seriesTv")
    },
    // Volevo Dare movimento allo slider attraveso il watch, guardando su una variabile, solamente che il watch ha la possibilità di guardare solo un elemento modificato
    // potrei allo usare il computed, semplicemente che quando lo metto modfica da solo lo slider, senza aver attivato nulla..

    // nextFilm(newValue){
    //   this.prevFilm +=2
    //   console.log(this.prevFilm)
    //   console.log(newValue)
    //   this.getSeriesFilm(this.urlFilm, "film", this.prevFilm, newValue)
    // }
  },
  mounted(){
    this.getSeriesFilm(this.urlFilm, "film");
    this.getSeriesFilm(this.urlSeries, "seriesTv")
  },
  methods:{    
    search(valueText, valueChange){
      this.searchText = valueText;
      this.value = valueChange;
      this.urlFilm = `https://api.themoviedb.org/3/search/movie?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT&query=${valueText}`;
      this.urlSeries = `https://api.themoviedb.org/3/search/tv?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT&query=${valueText}`;
      if(this.searchText == ""){
        this.urlFilm = `https://api.themoviedb.org/3/movie/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`;
        this.urlSeries = `https://api.themoviedb.org/3/tv/popular?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`;
      }
    },
    getSeriesFilm(API, array){
      const axios = require('axios')
      axios.get(API)
      .then(response => {
        // Ciclo for che posso utilizzare per ottonere solo 6 film alla volta, che saranno visti nello slider
        // for(let i = prev; i < next; i++){
          this[array] = (response.data.results) 
        // }
      })
    },
    // Questi sono i valori dello slider che cambiano ogni volta che premo sulla freccetta a destra del contenitore dei Film
    newValueSlider(next,prev){
      this.nextFilm = next;
      this.prevFilm = prev;
    }
  }
}
</script>

<style lang="scss">
  @import "./assets/style/general.scss";
  @import '~@fortawesome/fontawesome-free/css/all.css';
</style>
