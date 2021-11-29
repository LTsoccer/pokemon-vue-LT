<template>
<button id="load"
class="btn btn-outline-success"
@click="loadPokemon()">
Load Pokemon</button>
  <Header-Pokemon 
  @filter-pokemon="filter"/>
  <Party-Pokemon 
  :partyPokemon="partyPokemon"
  @remove-pokemon="remove" />
  <Filtered-Pokemon 
  :filteredPokemon="filteredPokemon"
  @add-pokemon="add"
  @clear-pokemon="clear" />
  <All-Pokemon 
  :allPokemon="allPokemon"
  @add-pokemon="add" />
</template>

<script>
import PartyPokemon from './components/PartyPokemon.vue'
import AllPokemon from './components/AllPokemon.vue'
import HeaderPokemon from './components/HeaderPokemon.vue'
import FilteredPokemon from './components/FilteredPokemon.vue'
const getPokemon = async function (id) {
    // get pokemon data from pokeapi
    const url = `https://pokeapi.co/api/v2/pokemon/${id}`;
  
    const response = await fetch(url);
    const data = await response.json();
    return data;
    
    //createPokemonCard( data );
  };

  const colors = {
    fire: '#fd7d24',
    grass: '#9bcc50',
    electric: '#eed535',
    water: '#4592c4',
    ground: '#ab9842',
    rock: '#a38c21',
    fairy: '#fdb9e9',
    poison: '#b97fc9',
    bug: '#729f3f',
    dragon: '#53a4cf',
    psychic: '#f366b9',
    flying: '#3dc7ef',
    fighting: '#d56723',
    normal: '#a4acaf',
    ice: '#51c4e7',
    ghost: '#7b62a3',
    dark: '#707070',
    steel: '#9eb7b8'
};

export default {
  name: 'App',
  components: {
    PartyPokemon,
    AllPokemon,
    HeaderPokemon,
    FilteredPokemon
  },
  data() {
    return {
      partyPokemon: [],
      allPokemon: [],
      filteredPokemon: []
    }
  },
  methods: {
    async loadPokemon() {
      // load all pokemon from API and save into all pokemon
      const pokemon_count = 200;
      let pokemon = [];
      for (let i = 1; i <= pokemon_count; i++) {
        let p = await getPokemon(i);

      if (p.name === "mr-mime"){
          p.uppername = "Mr. Mime";
      }

      p.uppername = p.name[0].toUpperCase() + p.name.slice(1);
      p.type1 = this.pokemonTypeString(p);
      p.guid = this.getGUID();
      p.gradient = this.getGradient(p);
      p.source = p.sprites.other['official-artwork'].front_default;
        pokemon.push(p);
      }

      pokemon.forEach( p => {
          this.allPokemon.push(p);
      });
    },
    pokemonTypeString(pokemon) {
      if (pokemon.types.length > 1) {
        return `${pokemon.types[0].type.name} / ${pokemon.types[1].type.name}`;
      } else {
        return `${pokemon.types[0].type.name}`;
      }
    },
    getGradient(pokemon) {
        const type1 = pokemon.types[0].type.name
        pokemon.color1 = colors[type1];
        if (pokemon.types.length > 1) {
            const type2 = pokemon.types[1].type.name
    pokemon.color2 = colors[type2];
        }
        else {
            pokemon.color2 = colors[type1];
        }
        return "linear-gradient(to right bottom," + pokemon.color1 + ", " + pokemon.color2 + ")";
    },
      remove(name) {
        this.partyPokemon = this.partyPokemon.filter (p => p.name != name);
        this.name = "";
      },
      getGUID() {
      return Math.floor(Math.random()* 1000000);
    },
    filter(value) {

        this.filteredPokemon = [];
      // set filteredPokemon to matching pokemon based on search query
      this.allPokemon.forEach( p => {
          console.log(value);
          console.log(p.name);
          if (p.types.length > 1) {
            if (p.types[1].type.name == value) {
                const pokemonCopy = {...p};
          pokemonCopy.guid = this.getGUID();
          console.log(p.name);
          console.log(pokemonCopy.guid);
          this.filteredPokemon.push(  pokemonCopy );
            }}
        if (p.id.toString().includes(value.toString())) {
            const pokemonCopy = {...p};
          pokemonCopy.guid = this.getGUID();
          console.log(p.name);
          console.log(pokemonCopy.guid);
          this.filteredPokemon.push(  pokemonCopy );
        } 
        else if (p.name.includes(value.toString().toLowerCase()) || p.types[0].type.name.includes(value.toString().toLowerCase())) {
            const pokemonCopy = {...p};
          pokemonCopy.guid = this.getGUID();
          console.log(p.name);
          console.log(pokemonCopy.guid);
          this.filteredPokemon.push(  pokemonCopy );
          }
      });
    },
    clear() {
      this.filteredPokemon = [];
    },
      add(name) {
        if (this.partyPokemon.length == 6) {
        alert("You can only add 6 Pokemon to your party.");
      }
      else {
        this.allPokemon.forEach( p => {
          if (p.name.toString().toLowerCase() == name.toString().toLowerCase()) {
            if (this.partyPokemon.length > 0) {
              var same = "false";
              this.partyPokemon.forEach( poke => {
                if (poke.name == name) {
                  alert("You can't add a Pokemon to your party that is already in your party.");
                  same = "true";
                }});
                if(same == "false"){
                  const pokemon = {...p};
                  pokemon.guid = this.getGUID();
                  this.partyPokemon.push(  pokemon );}
          }
          else {
            const pokemon = {...p};
            pokemon.guid = this.getGUID();
            this.partyPokemon.push(  pokemon );
          }
          }
        })
      }
      this.name = "";
    },
    mounted() {
    let bootstrap = document.createElement('script')
    bootstrap.setAttribute('src', 'https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/js/bootstrap.bundle.min.js')
    document.head.appendChild(bootstrap)
  }
}
}
</script>

<style>
@import "https://cdn.jsdelivr.net/npm/bootstrap@5.0.2/dist/css/bootstrap.min.css";
body {
  padding:15px;
  margin: 5px;}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  margin-top: 60px;
}
#load {
  margin-top: 10px;
  margin-bottom: 5px;
  text-align: center;
  font-size: 1.5em;
}
</style>
