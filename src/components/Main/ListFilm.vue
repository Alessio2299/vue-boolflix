<template>
  <div class="container">
    <h2>film</h2>
    <div class="containerCard">
      <div class="button">
        <i class="next fas fa-chevron-circle-right"></i>
        <i class="prev fas fa-chevron-circle-left"></i>
      </div>
      <span class="nothingResult" v-if="arrayFilm.length == 0">Non esistono risultati per questa ricerca</span>
       <CardFilm v-else v-for="(film,index) in arrayFilm" :key="index" :object="film" />
    </div>
  </div>
</template>

<script>
  import CardFilm from "./CardFilm.vue"
  export default {
    name: "ListFilm",
    data(){
      return{
      }
    },
    components:{
      CardFilm
    },
    props:{
      arrayFilm: Array
    },
    methods:{
    }
  }
</script>

<style scoped lang="scss">
  @import "../../assets/style/containerCard.scss";
  .nothingResult{
    font-size: 25px;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-transform: uppercase;
  }
</style>