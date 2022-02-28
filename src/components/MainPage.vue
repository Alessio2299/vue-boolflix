<template>
  <main>
    <ListFilm @next="valueSlider" :arrayFilm="listFilm" :value="value"/>
    <ListSerie :arraySerieTv="listTv" :value="value"/>
  </main>
</template>

<script>
  import ListFilm from "./Main/ListFilm.vue"
  import ListSerie from "./Main/ListSerie.vue"

  export default {
    name: "MainPage",
    data(){
      return{
        nextSliderFilm: "",
        prevSliderFilm: ""
      }
    },
    props:{
      listFilm: Array,
      listTv: Array,
      value: Number
    },
    components: {
    ListFilm,
    ListSerie
    },
    methods:{
      valueSlider(nextValue,prevValue){
        this.nextSliderFilm = nextValue;
        this.prevSliderFilm = prevValue;
        this.$emit("valueSliderFilm", this.nextSliderFilm, this.prevSliderFilm)
      }
    }
  }
</script>

<style scoped lang="scss">
  main{
    height: calc(100% - 77px);
    background-color: rgb(26, 26, 26);
    padding-top: 30px;
    
  }
</style>