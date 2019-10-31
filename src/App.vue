<template>
  <div id="app">
    <Header />
    <div class="flex-container">
      <div v-for="pokemon in pokemons" :key="pokemon.id" id="card" @click='showDetails($event)'>
        <cName :pokeName="pokemon.name" :pokeId="pokemon.id" />
        <cImage :imgUrl="pokemon.img" />
      </div>
    </div>
  </div>
</template>

<script>
import cImage from "./components/CardImage";
import cName from "./components/CardName";
import Header from "./components/Header";
import axios from "axios";

export default {
  name: "app",
  data() {
    return {
      pokemons: []
    };
  },
  components: {
    cImage,
    cName,
    Header
  },
  async created() {
    //add async and awaits
    for (var i = 1; i <= 4; ++i) {
      await axios.get("https://pokeapi.co/api/v2/pokemon/" + i).then(response => {
        this.pokemons.push({
          id: response.data.id,
          name: response.data.name.toUpperCase(),
          img: response.data.sprites.front_default
        });
      })
      .catch(e => {
        console.log(e);
      });
    }
  },
  methods: {
    showDetails(e) {
      console.log(e);
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
  align-content: flex-end;
  justify-content: left;
  margin: 8px;
}


#card {
  // flex: 1 0 31%; /* explanation below */
  margin: 5px;
  width: calc(100% * (1/3) - 9px - 1px);
}
</style>
