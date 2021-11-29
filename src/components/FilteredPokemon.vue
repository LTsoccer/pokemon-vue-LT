<template>
  <div>
      <div id="filter">
          <div class="inline">
        <h2>Filtered Pokemon</h2>
        <button class="btn btn-outline-success same" id="clearButton" type="button" @click="clear()">Clear Results</button>
        </div>
        <div id="filtered-pokemon">
            <PokemonCard 
            v-for="p in filteredPokemon" 
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
name: "FilteredPokemon",
data() {
      return {
        action: ""
      }
    },
    props: {
        filteredPokemon: Array
    },
    components: {
      PokemonCard
    },
    methods: {
        clear() {
            this.$emit("clear-pokemon");
        },
        addP(name) {
        this.$emit("add-pokemon", name);
      }
    }
}
</script>

<style>
#filtered-pokemon {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
.inline {
    display: flex;
    justify-content: space-between;
  }
</style>