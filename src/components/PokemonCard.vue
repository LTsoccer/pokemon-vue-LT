<template>
  <div class="pokemon" @click="alter" :style="{background: pokemon.gradient}">
            <!-- <a href="#" id="${pokemon.id}"> Favorite </a></div> -->
            <div class="img-container">
                <!-- <p>{{ pokemon.sprites}}</p> -->
                <!--<img src="https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/${pokemon.id}.png"" alt="${name}">-->
                <img
                  :src="pokemon.source"
                />
              </div>
            <div class="info">
              <span class="number">#{{pokemon.id}}</span>
              <h3 class="name">{{pokemon.uppername}}</h3>
              <small class="type"
                >Type:
                <span>
                  {{ pokemon.type1 }}
                </span>
              </small>
            </div>
          </div>
</template>

<script>
export default {
    name: "PokemonCard",
    props: {
        pokemon: Object,
        action: String
    },
    methods: {
      alter () {
        this.$emit("alter-pokemon", this.pokemon.name);
      }
    }

}
</script>

<style>
.pokemon {
    display: flex;
    flex-direction: column;
    align-items: center;
    flex-basis: 15%;
    background-color: #eee;
    border-radius: 10px;
    box-shadow: 0 3px 15px rgba(100, 100, 100, 0.5);
    margin: 10px;
    padding: 20px;
    text-align: center;
    transform: scale(1.0);
    transition: all 0.2s;
    cursor: pointer;
  }
  
  .pokemon:hover {
    transform: scale(1.05);
  }
  
  .pokemon .img-container {
    background-color: rgba(255, 255, 255, 0.5);
    border-radius: 50%;
    width: 100px;
    height: 100px;
    text-align: center;
  
  }
  
  .pokemon .img-container img {
    /* max-width: 90%; */
    width:120%;
    margin-top: 00px;
  }
  
  .pokemon .info {
    margin-top: 20px;
  }
  
  .pokemon .info .number {
    background-color: rgba(0, 0, 0, 0.1);
    padding: 5px 10px;
    border-radius: 10px;
    font-size: 0.8em;
  }
  
  .pokemon .info .name {
    font-family: 'Playfair Display', serif;
    font-weight: 400;
    margin: 15px 0 7px;
    letter-spacing: 1px;
  }
  
  .pokemon .info small {
    font-size: 0.7em;
    text-transform: capitalize;
    font-weight: 200;
  }
</style>