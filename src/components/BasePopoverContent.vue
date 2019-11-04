<template>
  <div
    class="vue-tour-popover-content"
    ref="PopoverContent"
    tabindex="-1"
    @keydown.esc="closePopover"
  >
    <div class="vue-tour-popover-content__header">
      <p>{{ pokemon.name }}</p>
      <img :src='pokemon.img'>
    </div >
      <p>{{ pokemon.flavor_text }}</p>
  </div>
</template>
<script>
export default {
  data() {
    return {
      descriptions: "Vue is Awesome!",
      step: 0
    };
  },
  props: [
    'pokemon'
  ],
  computed: {
    currentDescription() {
      return this.descriptions;
    },


  },

  methods: {
    closePopover() {
      this.$emit("closePopover");
    }
  },

  mounted() {
    this.$refs.PopoverContent.focus();
  }
};
</script>


<style lang="scss" scoped>
.vue-tour-popover-content {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 400px;
  background: white;
  padding:15px;

  &__header {
    width: 100%;
    border-bottom: solid 1px #000;
    margin-bottom: 20px;
  }

  &__actions {
    display: flex;
    justify-content: space-around;
    width: 100%;
    margin: 40px 0 20px;
  }

  &__button {
    background-color: #41B883;
    border: none;
    color: white;
    padding: 15px 32px;
    text-align: center;
    text-decoration: none;
    display: inline-block;
    font-size: 16px;
    border-radius: 4px;

    &.hidden {
      visibility: hidden;
    }
  }
}
</style>
