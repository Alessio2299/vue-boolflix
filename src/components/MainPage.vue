<template>
  <main>
    <ListFilm :arrayFilm="listFilm"/>
    <ListSerie :arraySerieTv="listTv"/>
  </main>
</template>

<script>
  import ListFilm from "./Main/ListFilm.vue"
  import ListSerie from "./Main/ListSerie.vue"

  export default {
    name: "MainPage",
    data(){
      return{
      }
    },
    props:{
      listFilm: Array,
      listTv: Array,
    },
    components: {
    ListFilm,
    ListSerie
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