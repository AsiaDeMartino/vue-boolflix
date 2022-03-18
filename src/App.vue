<template>
  <div id="app">
      <SearchBar @cerca="cerca" />
      <div>
        <ul class="d-flex mt-5 justify-content-center flex-wrap gap-5">
          <MyCard v-for="(item,i) in film" :key="i" :item="item" />
        </ul>
      </div>
  </div>
</template>

<script>
import axios from 'axios';
import "bootstrap";
import "bootstrap/dist/css/bootstrap.min.css";

import SearchBar from './components/SearchBar.vue'
import MyCard from './components/MyCard.vue'


export default {
  name: 'App',
  components: {
    SearchBar,
    MyCard,
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

</style>
