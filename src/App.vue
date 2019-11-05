<template>
  <div id="app">
    <Header />

    <div class="flex-container">
      <div v-for="pokemon in pokemons" :key="pokemon.id" id="card">
        <b-button :id="getId(pokemon.id)">
          <cName :pokeName="pokemon.name" :pokeId="pokemon.id" />
          <cImage :imgUrl="pokemon.img" />
        </b-button>
        <b-popover :target="getId(pokemon.id)" triggers="hover">
          <BasePopoverContent :pokemon="pokemon" @closePopover="isPopoverVisible = false" />
        </b-popover>
      </div>
    </div>
  </div>
</template>

<script>
import BasePopoverContent from "@/components/BasePopoverContent";
import cImage from "./components/CardImage";
import cName from "./components/CardName";
import Header from "./components/Header";
import POKEMON_DATA from "./assets/pokedata.json";

export default {
  name: "App",
  components: {
    BasePopoverContent,
    cImage,
    cName,
    Header
  },
  pokemons: [],
  data() {
    return {
      popoverPokemon: {
        name: "",
        flavor_text: "",
        img: ""
      }
    };
  },
  created() {
    this.pokemons = POKEMON_DATA;
  },

  methods: {
    getId(id) {
      return "popover-target-" + id;
    }
  }
};
</script>



<style lang="scss">
body {
  background: pink;
  margin: 0px;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.flex-container {
  display: flex;
  flex-direction: row;
  flex-flow: row wrap;
  // align-content: flex-end;
  justify-content: left;
  margin: 8px;
}

#card {
  margin: 40px;
  width: calc(100% * (1 / 3) - 80px - 1px);
}

button {
  width: 100%;
  margin: 0;
  background: #cfc8bb;
}
</style>
