<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark fixed-top">
        <div class="container-fluid">
          <h3>Pokedex</h3>
          <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarSupportedContent">
            <form class="d-flex"  @submit.prevent="filterPokemon(value)">
              <div class="input-group mb-3">
              <input id="search" class="form-control" v-model="value" type="text" placeholder="Search by name, type, or id" aria-label="Search" aria-describedby="searchButton">
              <button class="btn btn-outline-success" id="searchButton" type="button" @click="filterPokemon(value)">Search</button>
            </div>
            </form>
          </div>
        </div>
      </nav>
</template>

<script>
export default {
  name: "HeaderPokemon",
  methods: {
        filterPokemon(value) {
        this.$emit("filter-pokemon", value);
      }
    }
}
</script>

<style>
form {
  margin-top: 10px;
  margin-left: 50px;
}
nav p {
  color: white;
}

nav h3 {
  color: white;
}
</style>