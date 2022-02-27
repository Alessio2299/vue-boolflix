<template>
  <div class="container">
    <h2>serie Tv</h2>
    <div class="containerCard">
      <div class="button">
        <i class="next fas fa-chevron-circle-right"></i>
        <i class="prev fas fa-chevron-circle-left"></i>
      </div>
      <CardSeries v-for="(serie,index) in arraySerieTv" :key="index" :object="serie"/>

    </div>
  </div>
</template>

<script>
  import CardSeries from "./CardSeries.vue"
  export default {
    name: "ListSerie",
    components:{
      CardSeries
    },
    props:{
      arraySerieTv: Array
    }
  }
</script>

<style scoped lang="scss">
  @import "../../assets/style/containerCard.scss";
</style>