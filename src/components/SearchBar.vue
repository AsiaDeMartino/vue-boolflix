<template>
  <div class="search d-flex justify-content-end p-4">
    <input class="form-control me-3" type="search" placeholder="Search">
    <button class="btn btn-outline-light" type="submit">Search</button>

  </div>
</template>

<script>

export default {
  name: 'SearchBar',

}
</script>

<style lang="scss" scoped>
.search{
  height: 10vh;
  background-color: rgba(white, 0.1);
  input{
    width: 25%;
  }
}
</style>
