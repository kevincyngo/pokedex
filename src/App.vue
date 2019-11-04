<template>
  <div id="app">
    <Header />

    <div class="flex-container">
      <div v-for="pokemon in pokemons" :key="pokemon.id" id="card" @click="openPopover(pokemon, pokemon.id)">
        <cName :pokeName="pokemon.name" :pokeId="pokemon.id" />
        <cImage :imgUrl="pokemon.img" />
      </div>
          <BasePopover
      v-if="isPopoverVisible"
      :popover-options="popoverOptions"
      @closePopover="closePopover"
    >
        <BasePopoverContent :pokemon="popoverPokemon" @closePopover="isPopoverVisible = false" />
    </BasePopover>
    </div>
  </div>

</template>

<script>
import BasePopover from "./components/BasePopover";
import BasePopoverContent from "@/components/BasePopoverContent";
import cImage from "./components/CardImage";
import cName from "./components/CardName";
import Header from "./components/Header";
import axios from "axios";

var pokemonAPI = 'https://pokeapi.co/api/v2/pokemon/';
var pokemonSpeciesAPI = 'https://pokeapi.co/api/v2/pokemon-species/';

export default {
  name: "App",
  components: {
    BasePopover,
    BasePopoverContent,
    cImage,
    cName,
    Header
  },



  data() {
    return {
      isPopoverVisible: false,
      popoverOptions: {
        popoverReference: null,
      
        offset: "0,0"
      },
      pokemons: [],
      popoverPokemon: {
        name: "",
        flavor_text: "",
        img: "",
      }
    };
  },
  async created() {
    //add async and awaits
    for (var i = 1; i <= 151; ++i) {
      await axios
        .get(pokemonAPI + i)
        .then(response => {
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
  mounted() {
    this.popoverOptions.popoverReference = this.$refs.popoverReference;
  },

  methods: {
    closePopover() {
      this.isPopoverVisible = false;
      console.log("close");
    },

    async openPopover(pokemon, id) {
      this.isPopoverVisible = true;
      await axios
        .get(pokemonSpeciesAPI + id)
        .then(response => {
          this.popoverPokemon = {
            name : pokemon.name,
            flavor_text : response.data.flavor_text_entries[1].flavor_text,
            img : pokemon.img
          }
        })
        .catch(e => {
          console.log(e);
        });
    },
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
  margin: 40px;
  width: calc(100% * (1 / 3) - 80px - 1px);
}
</style>
