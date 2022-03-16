<template>
  <div id="app">
      <SearchBar @cerca="cerca" />
      <div>
        <ul>
          <li v-for="(item,i) in film" :key="i">
            <ol>{{item.title}}</ol>
            <ol>{{item.original_title}}</ol>
            <ol ><img :src="bandiera(item.original_language)" alt="">    {{item.original_language}}</ol>
            <ol>{{item.vote_average}}</ol>
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
      
    },
    bandiera: function(lingua){
      if (lingua == 'en') {
        lingua = 'gb';
        return ('https://flagcdn.com/16x12/' + lingua + '.png')
      } else {
        return ('https://flagcdn.com/16x12/' + lingua + '.png')
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  background-color: rgb(26, 26, 26);
  height: 100vh;
  overflow: scroll;
  color: white;
}
</style>
