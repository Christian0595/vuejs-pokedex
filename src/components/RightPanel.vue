<template>
  <div class="panel right-panel">
    <div class="panel-row">
      <div class="screen stats">
        <div class="stat-line">Velocidad.............{{pokemon.data.stats[0].base_stat}}</div>
        <div class="stat-line">Defensa especial...{{pokemon.data.stats[1].base_stat}}</div>
        <div class="stat-line">Ataque especial....{{pokemon.data.stats[2].base_stat}}</div>
        <div class="stat-line">Defensa...........{{pokemon.data.stats[3].base_stat}}</div>
        <div class="stat-line">Ataque............{{pokemon.data.stats[4].base_stat}}</div>
        <div class="stat-line">Salud................{{pokemon.data.stats[5].base_stat}}</div>
      </div>
      <div class="type-list">
        <div class="panel-header">Tipos</div>
        <div class="type-box">
          <div
            class="type"
            v-for="type in pokemon.data.types"
            :key="type.type.name"
            :class="type.type.name"
          >{{type.type.name}}</div>
        </div>
      </div>
    </div>
    <div class="panel-row panel-evo">
      <div>
        <div class="flex-center">
          <div class="evo-num">Hecho con:</div>
        </div>
        <div>
          <img src="../assets/logo.png" alt="pokemon" class="pokemon-sprite-small" />
          <div class>VueJS</div>
        </div>
      </div>
    </div>
    <div class="panel-row blue-buttons">
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
      <div class="blue-button"></div>
    </div>
    <div class="move-list" v-if="move">
      <div class="move-body move-screen screen">
        <div class="move-left">
          <div class="move-name">{{move.name}}</div>
          <div class="move-stat">Accuracy.....{{move.accuracy}}</div>
          <div class="move-stat">Power.........{{move.power}}</div>
          <div class="move-stat">PP............{{move.pp}}</div>
        </div>
        <div class="move-right">
          <div class="move-type">Type: {{move.type.name}}</div>
          <div
            class="move-learn"
          >Learn: Lvl {{pokemon.data.moves[moveIndex].version_group_details[0].level_learned_at}}</div>
        </div>
      </div>
      <div class="move-controls">
        <div class="move-arrow" @click="nextMove()">
          <i class="fas fa-caret-up"></i>
        </div>
        <div class="move-arrow" @click="prevMove()">
          <i class="fas fa-caret-down"></i>
        </div>
      </div>
    </div>
    <div class="panel-row controls">
      <div @click="$emit('prev');chargeMoves()" class="button"></div>
      <div>
        <input type="number" class="screen num-input" placeholder="1" v-model="pokemon_id" />
        <div class="submit" @click="$emit('goTo',pokemon_id);chargeMoves()"></div>
      </div>
      <div @click="$emit('next'); chargeMoves()" class="button"></div>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  props: {
    pokemon: Object,
    pokemon_id: Number
  },
  data() {
    return {
      moveIndex: 0,
      move: undefined
    };
  },
  created() {
    axios
      .get(this.$props.pokemon.data.moves[0].move.url)
      .then(response => (this.move = response.data));
  },
  watch: {
    moveIndex: function() {
      axios
        .get(this.$props.pokemon.data.moves[this.moveIndex].move.url)
        .then(response => (this.move = response.data));
    }
  },
  methods: {
    nextMove() {
      if (this.moveIndex < this.$props.pokemon.data.moves.length)
        this.moveIndex++;
    },
    prevMove() {
      if (this.moveIndex > 1) this.moveIndex--;
    },
    chargeMoves() {
      axios
        .get(this.$props.pokemon.data.moves[0].move.url)
        .then(response => (this.move = response.data));
    }
  }
};
</script>
<style scoped>
input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

input[type="number"] {
  -moz-appearance: textfield;
  padding: 0px;
}
</style>