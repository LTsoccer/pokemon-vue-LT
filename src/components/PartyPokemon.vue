<template>
  <div>
      <div id="party">
        <h2>Party</h2>
        <h4>{{ partyPokemon.length }} of 6 Pokemon in your party</h4>
        <div id="party-pokemon">
            <PokemonCard 
            v-for="p in partyPokemon" 
            :key="p.guid" 
            :pokemon="p"
            @alter-pokemon="removeP" />
            
          </div>
      </div>

  </div>
</template>

<script>

import PokemonCard from "./PokemonCard.vue"

export default {
    name: "PartyPokemon",
    data() {
      return {
        pGuid: 0,
        action: ""
      }
    },
    props: {
        partyPokemon: Array
    },
    components: {
      PokemonCard
    },
    methods: {
      removeP(name) {
        this.$emit("remove-pokemon", name);
      }
    }

}
</script>

<style>
#party-pokemon {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}
</style>