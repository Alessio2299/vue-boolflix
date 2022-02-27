<template>
  <div @click="nothingOverview" class="card">
    <div class="card-inner">
      <div class="card-front">
        <img :src="`https://image.tmdb.org/t/p/w342${object.poster_path}`" :alt="object.title">
      </div>
      <div class="card-back">
        <p><span>Titolo:</span> {{object.title}}</p>
        <p v-if="object.title != object.original_title"><span>Titolo Originale:</span> {{object.original_title}}</p>
        <p><span>Lingua:</span> {{object.original_language}}</p>
        <p><span>Voto:</span> {{object.vote_average}}</p>
        <p v-if="object.overview != ''"><span>Trama:</span> {{object.overview}}</p>
        <p v-else><span>Trama:</span> {{nothingOverview}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "CardFilm",
    data(){
      return{
        nothingOverview : "Nessuna trama disponibile",
      }
    },
    props:{
      object : Object
    }
  }
</script>

<style scoped lang="scss">
  .card{
    height: 100%;
    border: 2px solid rgb(26, 26, 26);
    display: inline-block;
    position: relative;
    perspective: 1000px;
    width: calc(100% / 6);
    .card-inner{
      transition: transform 2s;
      transform-style: preserve-3d;
    }
    &:hover .card-inner {
    transform: rotateY(180deg);
    }
    .card-inner{
      height: 100%;
      .card-front,
      .card-back{
        height: 100%;
        object-fit: cover;
        object-position: center;
        backface-visibility: hidden;
        width: 100%;
        overflow: hidden;
        img{
          height: 100%;
        }
      }
      .card-back{
      backface-visibility: hidden;
      position: absolute;
      background-color: #000;
      top: 0;
      left: 0;
      right: 0;
      height: 100%;
      overflow: auto;
      color: gray;
      font-size: 14px;
      line-height: 20px;
      padding: 10px;
      transform: rotateY(180deg);
        span{
          color: #fff;
          font-weight: bold;
        }
      }
    }
  }
</style>

  // .card{
  //   width: calc(100% / 6);
  //   height: 100%;
  //   border: 2px solid rgb(26, 26, 26);
  //   display: inline-block;
  //   position: relative;
  //   perspective: 1000px;
  //   &:hover .card-inner {
  //   transform: rotateY(180deg);
  //   } 
  //   .card-inner{
  //     transition: transform 2s;
  //     transform-style: preserve-3d;
  //   }
  //   .card-front{
  //     img{
  //     width: 100%;
  //     height: 100%;
  //     object-fit: cover;
  //     backface-visibility: hidden;
  //     }
  //   }
  //   .card-back{
  //     backface-visibility: hidden;
  //     position: absolute;
  //     background-color: #000;
  //     top: 0;
  //     left: 0;
  //     right: 0;
  //     height: 100%;
  //     overflow: auto;
  //     color: gray;
  //     font-size: 14px;
  //     line-height: 20px;
  //     padding: 10px;
  //     transform: rotateY(180deg);
  //     span{
  //       color: #fff;
  //       font-weight: bold;
  //     }
  //   }
  // }