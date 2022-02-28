<template>
  <div class="container">
    <h2>serie Tv</h2>
    <div class="containerCard">
      <div class="button">
        <i class="next fas fa-chevron-circle-right"></i>
        <i class="prev fas fa-chevron-circle-left"></i>
      </div>
      <span class="nothingResult" v-if="arraySerieTv.length == 0">Non esistono risultati per questa ricerca</span>
      <SingleCard v-else v-for="(serie,index) in arraySerieTv" :key="index" :object="serie"/>
    </div>
  </div>
</template>

<script>
  import SingleCard from "./SingleCard.vue"
  export default {
    name: "ListSerie",
    components:{
      SingleCard
    },
    props:{
      arraySerieTv: Array
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