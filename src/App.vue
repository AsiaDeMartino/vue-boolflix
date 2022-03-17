<template>
  <div id="app">
      <SearchBar @cerca="cerca" />
      <div>
        <ul class="d-flex mt-5 justify-content-center flex-wrap gap-5">
          <li v-for="(item,i) in film" :key="i">
            <img v-if="item.poster_path" :src="locandina(item.poster_path)" alt="">
            <img class="poster_placeholder" v-else src="./assets/poster-placeholder.png" alt="">
            <ol v-if="item.title">{{item.title}}</ol>
            <ol v-if="item.name">{{item.name}}</ol>
            <ol v-if="item.original_title">{{item.original_title}}</ol>
            <ol v-if="item.original_name">{{item.original_name}}</ol>
            <ol ><img :src="bandiera(item.original_language)" :alt="item.original_language"></ol>
            <ol>{{item.vote_average}}</ol>
            <ol class="stella">
              <span v-html="stellaPiena(item.vote_average)"></span>  <!-- piena -->
              <span v-html="stellaVuota(item.vote_average)"></span>   <!-- vuota -->
            </ol>
          </li>
        </ul>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";

import SearchBar from './components/SearchBar.vue'


export default {
  name: 'App',
  components: {
    SearchBar
  },
  data() {
    return {
      film: [],
    }
  }, 
  methods: {
    cerca: function (ricercaUtente) {
      console.log(ricercaUtente);
      axios.get('https://api.themoviedb.org/3/search/movie', {
        params: {
          api_key: '8fa780c148ee8959c5bfe762a4b106c2',
          query: ricercaUtente,
          language: 'it-IT',
        }
      })
      .then( res => {
        // console.log(res.data);
        this.film = res.data.results;
        console.log(this.film)
      })
      axios.get('https://api.themoviedb.org/3/search/tv', {
        params: {
          api_key: '8fa780c148ee8959c5bfe762a4b106c2',
          query: ricercaUtente,
          language: 'it-IT',
        }
      })
      .then( res => {
        // console.log(res.data);
        this.film.push(...res.data.results);
        console.log(this.film);
      })
      
    },
    bandiera: function(lingua){
      if (lingua == 'en') {
        lingua = 'gb';
        return ('https://flagcdn.com/16x12/' + lingua + '.png')
      } else {
        return ('https://flagcdn.com/16x12/' + lingua + '.png')
      }
    },
    locandina: function(immagine){
      return ('https://image.tmdb.org/t/p/w342' + immagine);
    },
    stellaPiena: function(voto){
      let stelle;
      stelle = parseInt(voto/2)
      return ('&#9733; '.repeat(stelle))
    },
    stellaVuota: function(voto){
      let stelle;
      stelle = 5 - parseInt(voto/2)
      return ('&#9734; '.repeat(stelle))
    }
  }
}
</script>

<style>
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: rgb(26, 26, 26);
  height: 100vh;
  overflow: scroll;
  color: white;
}

li{
  list-style: none;
}

.poster_placeholder{
  width: 342px;
}

.stella{
  color: gold;
}
</style>
