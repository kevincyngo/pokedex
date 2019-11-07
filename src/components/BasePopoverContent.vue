<template>
  <div class="vue-tour-popover-content" ref="PopoverContent" tabindex="-1">
    <div class="vue-tour-popover-content__header">
      <p>
        <span class="type" v-for="type in pokemon.type" :key="type">
          <!-- <img :src="getTypeImg(type)">   -->
          {{type}}
        </span> {{ pokemon.name }} the {{pokemon.genus}}
      </p>
    </div>
    <div class="vue-tour-popover-content__img">
      <img class="popover-img" :src="pokemon.img" />
    </div>
    <div class="flavor-text">
      <p>{{ pokemon.flavor_text }}</p>
    </div>
    <div class="pokemon-stats">
      <span class="stat" id="hp">HP: {{hp}}</span>
      <span class="stat" id="def">Defense: {{defense}}</span>
      <span class="stat" id="spd">Speed: {{speed}}</span>
      <span class="stat" id="atk">Attack: {{attack}}</span>
      <span class="stat" id="sp-def">Sp Def: {{sp_defense}}</span>
      <span class="stat" id="sp-atk">Sp Atk: {{sp_attack}}</span>
    </div>
  </div>
</template>
<script>
var SPEED = "speed";
var HP = "hp";
var ATTACK = "attack";
var DEFENSE = "defense";
var SP_ATTACK = "special-attack";
var SP_DEFENSE = "special-defense";

export default {
  name: "BasePopoverContent",
  data() {
    return {
      speed: "",
      hp: "",
      defense: "",
      attack: "",
      sp_attack: "",
      sp_defense: ""
    };
  },
  props: ["pokemon"],
  mounted() {
    var stats = this.pokemon.stats;
    for (var stat in stats) {
      if (stat == SPEED) {
        this.speed = stats[stat];
      } else if (stat == ATTACK) {
        this.attack = stats[stat];
      } else if (stat == DEFENSE) {
        this.defense = stats[stat];
      } else if (stat == HP) {
        this.hp = stats[stat];
      } else if (stat == SP_ATTACK) {
        this.sp_attack = stats[stat];
      } else if (stat == SP_DEFENSE) {
        this.sp_defense = stats[stat];
      }
    }
  },
  methods: {
    getType() {
      let str = "";
      for (let type of this.pokemon.type) {
        str += type + ", ";
      }
      return str.substring(0, str.length - 2);
    },
    getTypeImg(type) {
      console.log(type);
    }
  }
};
</script>


<style lang="scss" scoped>
.vue-tour-popover-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  width: 350px;
  height: 100%;
  background-color: azure;
  padding: 15px;
  border-radius: 10px;

  &__header {
    width: 100%;
    font-size: 20px;
    text-align: left;
  }

  &__img {
      border: solid 1px black;
  background-color: grey;
  border-radius: 10px;
  width:100%;
  }
}

.popover-img {
  width:250px;
  height:250px;
  padding: 10px;
}

.pokemon-stats {
  display: grid;
  grid-template-columns: 90px 90px 90px;
  grid-gap:20px 20px;
}


.stat {
  padding: 5px;
  background: rgb(2,0,36);
  background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(23,209,127,1) 0%, rgba(113,252,252,1) 100%);
  border-radius: 10px;
}

.type {
  font-size: 10px;
}

</style>
