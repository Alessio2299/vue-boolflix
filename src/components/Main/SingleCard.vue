<template>
  <div class="card">
    <div class="card-inner">
      <div class="card-front">
        <img v-if="object.poster_path != null" :src="`https://image.tmdb.org/t/p/w342${object.poster_path}`" :alt="object.title">
        <img v-else src="https://www.edizionicantagalli.com/wp-content/uploads/2020/01/Copertina-non-disponibile.jpg" :alt="object.title">
      </div>
      <div class="card-back">
        <p v-if="object.title != undefined">
          <span>Titolo:</span> 
          {{object.title}}
        </p>
        <p v-else>
          <span>Titolo:</span> 
          {{object.name}}
        </p>
        <p v-if="object.name != object.original_name">
          <span>Titolo Originale:</span> 
          {{object.original_name}}
        </p>
        <p>
          <span>Lingua: </span>
          <img class="flag" v-if="flags.includes(object.original_language)" :src="require (`../../assets/img/flag-${object.original_language}.svg`)" alt="en">
          <span v-else>{{object.original_language}}</span>
        </p>
        <span class="rating">Voto: 
          <StarRating :star-size="10" :show-rating="false" :rating="object.vote_average / 2" :read-only="true"/>
        </span>
        <p v-if="object.overview != ''">
          <span>Trama: </span> 
          {{object.overview}}
        </p>
        <p v-else>
          <span>Trama: </span> 
          {{nothingOverview}}
        </p>
        <p>
          <span>Cast: </span>
          <span class="genre" v-if="getInfoCast.length == 0">Nessun cast disponibile</span>
          <span v-else class="actor" v-for="(actor,index) in getInfoCast.slice(0, 5)" :key="index">{{actor.name}},</span>
        </p>
        <p>
          <span>Genere: </span>
          <span class="genre" v-if="getInfoGenre.length == 0">Nessun genere disponibile</span>
          <span v-else class="genre" v-for="(genre,index) in getInfoGenre" :key="index">{{genre.name}},</span>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
  import StarRating from 'vue-star-rating'

  export default {
    name: "SingleCard",
    data(){
      return{
        nothingOverview : "Nessuna trama disponibile",
        flags: ["en", "it", "es"],
        cast: [],
        genres:[]
      }
    },
    computed:{
      getInfoCast(){
        this.getInfo(`https://api.themoviedb.org/3/${this.type}/${this.object.id}/credits?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`, "cast", "cast")
        return this.cast
      },
      getInfoGenre(){
        this.getInfo(`https://api.themoviedb.org/3/${this.type}/${this.object.id}?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`, "genres", "genres")
        return this.genres
      }
    },
    mounted(){
      this.getInfo(`https://api.themoviedb.org/3/${this.type}/${this.object.id}/credits?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`, "cast", "cast")
      this.getInfo(`https://api.themoviedb.org/3/${this.type}/${this.object.id}?api_key=0c96dc1900571df6b92cf3cd3536e18b&language=it-IT`, "genres", "genres")
    },
    components:{
      StarRating,
    },
    props:{
      object : Object,
      value: Number,
      type: String
    },
    methods:{
      getInfo(API,array, interested){
        const axios = require('axios')
        axios.get(API)
        .then(response => {
          this[array] = (response.data[interested])
        })
      }
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