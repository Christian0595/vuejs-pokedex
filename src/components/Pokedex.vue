<template>
  <div class="pokedex" v-if="pokemon.data && pokemon.species">
    <left-panel :pokemon_id="pokemon_id" :pokemon="pokemon" />
    <divider />
    <right-panel v-on:goTo="pokemon_id=$event" v-on:prev="pokemon_id>1?pokemon_id--:pokemon_id" v-on:next="pokemon_id<807?pokemon_id++:pokemon_id" :pokemon="pokemon" :pokemon_id="pokemon_id" />
  </div>
</template>
<script>
import axios from "axios";
import LeftPanel from "./LeftPanel.vue";
import Divider from "./Divider.vue";
import RightPanel from "./RightPanel.vue";
export default {
  components: {
    LeftPanel,
    Divider,
    RightPanel
  },
  data() {
    return {
      pokemon: {
        data: undefined,
        species: undefined
      },
      pokemon_id: 1
    };
  },
  created() {
    axios
      .get("https://pokeapi.co/api/v2/pokemon/" + this.pokemon_id)
      .then(response => (this.pokemon.data = response.data));
    axios
      .get("https://pokeapi.co/api/v2/pokemon-species/" + this.pokemon_id)
      .then(response => (this.pokemon.species = response.data));
  },
  watch: {
    pokemon_id: function() {
      axios
        .get("https://pokeapi.co/api/v2/pokemon/" + this.pokemon_id)
        .then(response => (this.pokemon.data = response.data));
      axios
        .get("https://pokeapi.co/api/v2/pokemon-species/" + this.pokemon_id)
        .then(response => (this.pokemon.species = response.data));
    }
  }
};
</script>   