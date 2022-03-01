<template>
  <div class="container">
    <h2>serie Tv</h2>
    <div class="containerCard">
      <div class="button">
        <i @click="next()" v-if="nextSlider < arraySerieTv.length" class="next fas fa-chevron-circle-right"></i>
        <i @click="prev()" v-if="prevSlider > 0" class="prev fas fa-chevron-circle-left"></i>
      </div>
      <span class="nothingResult" v-if="arraySerieTv.length == 0">Non esistono risultati per questa ricerca</span>
      <SingleCard 
        v-else 
        v-for="(serie,index) in arraySerieTv.slice(prevSlider, nextSlider)" 
        :key="index" 
        :object="serie" 
        :type="type"
      />
    </div>
  </div>
</template>

<script>
  import SingleCard from "./SingleCard.vue"
  export default {
    name: "ListSerie",
    data(){
      return{
        type: "tv",
        prevSlider: 0,
        nextSlider: 6,
      }
    },
    components:{
      SingleCard
    },
    props:{
      arraySerieTv: Array,
    },
    methods:{
      next(){
        this.nextSlider += 1 
        this.prevSlider += 1
      },
      prev(){
        this.nextSlider -= 1 
        this.prevSlider -= 1
      }
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