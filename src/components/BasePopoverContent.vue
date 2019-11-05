<template>
  <div
    class="vue-tour-popover-content"
    ref="PopoverContent"
    tabindex="-1"
  >
    <div class="vue-tour-popover-content__header">
      <p>{{ pokemon.name }} the {{pokemon.genus}}</p>
    </div >
    <div class="vue-tour-popover-content__img">
            <img class="popover-img" :src='pokemon.img'>

      </div>
      <p class="testing">{{ getType() }}</p>
      <p>{{ pokemon.flavor_text }}</p>

  </div>
</template>
<script>
export default {
  name: "BasePopoverContent",
  data() {
    return {
    };
  },
  props: [
    'pokemon'
  ],
  mounted() {
    console.log(this.pokemon);
  },
  methods: {
    getType() {
      let str = "";
      for (let type of this.pokemon.type) {
        console.log(type);
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
