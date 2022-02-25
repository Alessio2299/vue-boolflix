<template>
  <div class="card">
    <img :src="`https://image.tmdb.org/t/p/w342${object.poster_path}`" :alt="object.original_title">
  </div>
</template>

<script>
  export default {
    name: "CardComponent",
    props:{
      object : Object
    },
    methods:{
      // Prova per capire se l'errore era dovuto ad un tempo di caricamento della chiamata axios
      /*
      posterpath(){
        let time = '';
        setTimeout(() => 
          time = this.film.poster_path
        , 1000);
      }
      */
    }
  }
</script>

<style scoped lang="scss">
  .card{
    width: calc(100% / 6);
    height: 100%;
    background-color: hotpink;
    border: 2px solid rgb(26, 26, 26);
    img{
      width: 100%;
      height: 100%;
      object-fit: cover;
    }
  }
</style>