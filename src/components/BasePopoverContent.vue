<template>
  <div
    class="vue-tour-popover-content"
    ref="PopoverContent"
    tabindex="-1"
  >
    <div class="vue-tour-popover-content__header">
      <p>#{{pokemon.id}} {{ pokemon.name }} the {{pokemon.genus}}</p>
    </div >
    <div class="vue-tour-popover-content__img">
            <img class="popover-img" :src='pokemon.img'>

      </div>
      <p class="testing">{{ getType() }}</p>
      <p>{{ pokemon.flavor_text }}</p>
      HP: {{hp}}
      Defense: {{defense}}
      Speed: {{speed}}
      Attack: {{attack}}
      Special Defense: {{sp_defense}}
      Special Attack: {{sp_attack}}
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
  props: [
    'pokemon'
  ],
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
      return str.substring(0,str.length-2);
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
  width: 400px;
  background: white;
  padding:15px;
  border: solid 1px black;
  border-radius:10px;

  &__header {
    width: 100%;
    border-bottom: solid 1px #000;
    margin-bottom: 20px;
    font-size:20px;
    text-align:left;
  }

  &__actions {
    display: flex;
    justify-content: space-around;
    width: 100%;
    margin: 40px 0 20px;
  }

}

.popover-img{
  width:200px;
  height:200px;
  
}

.testing {
  width: 400px;
  border-top: solid 1px #000;
  padding-top:5px;
}

*{
  align-items: center;
}
</style>
