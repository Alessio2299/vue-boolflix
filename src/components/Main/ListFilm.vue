<template>
  <div class="container">
    <h2>film</h2>
    <div class="containerCard">
      <div class="button">
        <i class="next fas fa-chevron-circle-right"></i>
        <i class="prev fas fa-chevron-circle-left"></i>
      </div>
      <CardComponent @click="selectedFilm" v-for="(film,index) in arrayFilm" :key="index" :object="film" />
    </div>
  </div>
</template>

<script>
  import CardComponent from "./CardComponent.vue"
  export default {
    name: "ListFilm",
    components:{
      CardComponent
    },
    props:{
      arrayFilm: Array
    },
    methods:{
      selectedFilm(){
        console.log(this.arrayFilm);
      }
    }
  }
</script>

<style scoped lang="scss">
  @import "../../assets/style/containerCard.scss";
</style>