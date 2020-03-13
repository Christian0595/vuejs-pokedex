<template>
  <div class="panel" v-if="pokemon.data">
    <div class="pokemon-name screen">
      {{pokemon.data.name}}
      <span class="name-no">no. {{pokemon.data.id}}</span>
    </div>
    <div>
      <img class="pokemon-sprite" :src="returnSprite" alt="pokemon" />
      <div class="sprite-controls">
        <div
          @click="changeSprite('gender')"
          class="sprite-control sprite-controls-gender"
          v-show="!isMale"
        >
          <i class="fas fa-venus"></i>
        </div>
        <div
          @click="changeSprite('gender')"
          class="sprite-control sprite-controls-gender"
          v-show="isMale"
        >
          <i class="fas fa-mars"></i>
        </div>
        <div @click="changeSprite('shiny')" class="sprite-control sprite-controls-shiny">
          <span>shiny</span>
        </div>
        <!-- <div class="sprite-control sprite-controls-rotate">
          <i class="fas fa-undo"></i>
        </div> -->
      </div>
    </div>
    <div
      class="pokemon-description screen"
    >{{pokemon.species.flavor_text_entries.find(element => element.language.name === "es").flavor_text}}</div>
  </div>
</template>
<script>
export default {
  props: {
    pokemon: Object,
    pokemon_id: Number
  },
  data() {
    return {
      sprite: "front-default"
    };
  },
  methods: {
    changeSprite(sprite) {
      switch (sprite) {
        case "shiny":
          if (this.sprite === "front-default") this.sprite = "front-shiny";
          else if (this.sprite === "front-female")
            this.sprite = "front-shiny-female";
          else if (this.sprite === "front-shiny") this.sprite = "front-default";
          else if (this.sprite === "front-shiny-female")
            this.sprite = "front-female";
          break;
        case "gender":
          if (this.sprite === "front-default") this.sprite = "front-female";
          else if (this.sprite === "front-shiny") this.sprite = "front-shiny-female";
          else if (this.sprite === "front-female") this.sprite = "front-default";
          else if (this.sprite === "front-shiny-female") this.sprite = "front-shiny";

          break;
      }
    }
  },
  computed: {
    returnSprite: function() {
      if (this.sprite === "front-default")
        return this.$props.pokemon.data.sprites.front_default;
      else if (this.sprite === "front-shiny")
        return this.$props.pokemon.data.sprites.front_shiny;
      else if (this.sprite === "front-female")
        return this.$props.pokemon.data.sprites.front_female != null
          ? this.$props.pokemon.data.sprites.front_female
          : this.$props.pokemon.data.sprites.front_default;
      else if (this.sprite === "front-shiny-female")
        return this.$props.pokemon.data.sprites.front_shiny_female != null
          ? this.$props.pokemon.data.sprites.front_shiny_female
          : this.$props.pokemon.data.sprites.front_default;
      return this.$props.pokemon.data.sprites.front_default;
    },
    isMale: function() {
      var fas = true;
      if ((this.sprite == "front-default") | (this.sprite == "front-shiny"))
        fas = true;
      else if (
        (this.sprite == "front-female") |
        (this.sprite == "front-shiny-female")
      )
        fas = false;
      return fas;
    }
  }
};
</script>