<template>
  <div class="container">
    <h2>film</h2>
    <div class="containerCard">
      <div class="button">
        <i class="next fas fa-chevron-circle-right"></i>
        <i class="prev fas fa-chevron-circle-left"></i>
      </div>
      <CardFilm v-for="(film,index) in arrayFilm" :key="index" :object="film" />
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
</style>