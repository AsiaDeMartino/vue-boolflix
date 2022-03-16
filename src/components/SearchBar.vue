<template>
  <div class="search d-flex justify-content-between p-4">
    <img src="../assets/logo-netflix.png" alt="">
    <div class="d-flex">
      <input @keyup.enter="cercaFilm" v-model="inputSearch" class="form-control me-3" type="search" placeholder="Search">
      <button @click="cercaFilm" class="btn btn-outline-light" type="submit">Search</button>
    </div>
  </div>
</template>

<script>

export default {
  name: 'SearchBar',
  data() {
    return {
      inputSearch: '',
    }
  },
  methods: {
    cercaFilm: function() {
      this.$emit('cerca',this.inputSearch)
    }
  }

}
</script>

<style lang="scss" scoped>
.search{
  height: 10vh;
  background-color: rgba(white, 0.1);

  input{
    width: 300px;
  }

  img{
    height: 6vh;
  }

}
</style>
