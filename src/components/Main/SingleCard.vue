<template>
  <div class="card">
    <div class="card-inner">
      <div class="card-front">
        <img v-if="object.poster_path" :src="`https://image.tmdb.org/t/p/w342${object.poster_path}`" :alt="title()">
        <img v-else :src="require ('../../assets/img/Copertina-non-disponibile.jpeg')" :alt="title()">
      </div>
      <div class="card-back">
        <div>
          <span>Titolo:</span> 
          {{title()}}
        </div>
        <div v-if="object.original_title != object.title || object.original_name != object.name">
          <span>Titolo Originale:</span> 
          {{originalTitle()}}
        </div>
        <div>
          <span>Lingua: </span>
          <img class="flag" v-if="flags.includes(object.original_language)" :src="require (`../../assets/img/flag-${object.original_language}.svg`)" alt="en">
          <span v-else>{{object.original_language}}</span>
        </div>
        <span class="rating">Voto: 
          <StarRating :star-size="10" :show-rating="false" :rating="object.vote_average / 2" :read-only="true"/>
        </span>
        <div v-if="object.overview != ''">
          <span>Trama: </span> 
          {{object.overview}}
        </div>
        <div v-else>
          <span>Trama: </span> 
          Nessuna trama disponibile.
        </div>
        <div>
          <span>Cast: </span>
          <span class="actor" v-if="getInfoCast.length == 0">Nessun cast disponibile</span>
          <span v-else class="actor" v-for="(actor,index) in getInfoCast.slice(0, 5)" :key="index">{{actor.name}},</span>
        </div>
        <div>
          <span>Genere: </span>
          <span class="genre" v-if="getInfoGenre.length == 0">Nessun genere disponibile</span>
          <span v-else class="genre" v-for="(genre,index) in getInfoGenre" :key="index">{{genre.name}},</span>
        </div>
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
        flags: ["en", "it", "es"],
        cast: [],
        genres:[],
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
      type: String,
    },
    methods:{
      getInfo(API,array, interested){
        const axios = require('axios')
        axios.get(API)
        .then(response => {
          this[array] = (response.data[interested])
        })
      },
      title(){
        if(this.object.title){
          return this.object.title
        }else{
          return this.object.name
        }
      },
      originalTitle(){
        if(this.object.original_title){
          return this.object.original_title
        }else{
          return this.object.original_name
        }
      }
    }
  }
</script>

<style scoped lang="scss">
  @import "../../assets/style/card.scss";
</style>