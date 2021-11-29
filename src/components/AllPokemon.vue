<template>
  <div>
      <div id="all">
        <h2>All Pokemon</h2>
        <div id="all-pokemon">
            <PokemonCard 
            v-for="p in allPokemon" 
            :key="p.guid" 
            :pokemon="p"
            @alter-pokemon="addP" />
            
          </div>
      </div>

  </div>
</template>

<script>
import PokemonCard from "./PokemonCard.vue"
export default {
    name: "AllPokemon",
    data() {
      return {
        action: ""
      }
    },
    props: {
        allPokemon: Array
    },
    components: {
      PokemonCard
    },
    methods: {
        addP(name) {
            console.log(name);
        this.$emit("add-pokemon", name);
      }
    }
}
</script>

<style>
#all-pokemon {
  height: 50vh;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;

}
</style>