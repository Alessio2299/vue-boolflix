<template>
  <div @click="nothingOverview" class="card">
    <div class="card-inner">
      <div class="card-front">
        <img v-if="object.poster_path != null" :src="`https://image.tmdb.org/t/p/w342${object.poster_path}`" :alt="object.title">
        <img v-else src="https://www.edizionicantagalli.com/wp-content/uploads/2020/01/Copertina-non-disponibile.jpg" :alt="object.title">
      </div>
      <div class="card-back">
        <p><span>Titolo:</span> {{object.name}}</p>
        <p v-if="object.name != object.original_name"><span>Titolo Originale:</span> {{object.original_name}}</p>
        <p><span>Lingua: </span><img class="flag" :src="flags.en" alt="en"></p>
        <span class="rating">Voto: <StarRating :star-size="10" :show-rating="false" :rating="object.vote_average / 2" :read-only="true"/></span>
        <p v-if="object.overview != ''"><span>Trama:</span> {{object.overview}}</p>
        <p v-else><span>Trama:</span> {{nothingOverview}}</p>
      </div>
    </div>
  </div>
</template>

<script>
  import StarRating from 'vue-star-rating'
  import FlagEn from '../../assets/img/flag-en.svg'
  import FlagIt from '../../assets/img/flag-es.svg'
  import FlagEs from '../../assets/img/flag-it.svg'

  export default {
    name: "CardSeries",
    data(){
      return{
        nothingOverview : "Nessuna trama disponibile",
        flags: {
          en : FlagEn,
          it : FlagIt,
          es : FlagEs
        }
      }
    },
    components:{
      StarRating,
    },
    props:{
      object : Object
    }
  }
</script>

<style scoped lang="scss">
  @import "../../assets/style/card.scss";
  .rating{
    display: flex;
    margin-right: 5px;
    width: 90px;
    justify-content: space-between;
  }
  .flag{
    width: 20px;
    line-height: 40px;
    vertical-align: middle;
    margin-left: 5px;
  }
</style>