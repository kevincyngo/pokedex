<template>
  <div>
    <div ref="basePopoverContent" class="base-popover">
      <slot/>
    </div>

    <div ref="basePopoverOverlay" class="base-popover__overlay" @click.stop="destroyPopover"/>
  </div>
</template>

<script>

export default {
  name: "BasePopover",

  props: {
    popoverOptions: {
      type: Object,
      required: true
    }
  },

  data() {
    return {
      popperInstance: null
    };
  },



  methods: {

    destroyPopover() {
      if (this.popperInstance) {
        this.popperInstance.destroy();
        this.popperInstance = null;
        this.$emit("closePopover");
      }
    },

    updateOverlayPosition() {
      const overlayElement = this.$refs.basePopoverOverlay;
      const overlayPosition = overlayElement.getBoundingClientRect();

      overlayElement.style.transform = `translate(-${overlayPosition.x}px, -${
        overlayPosition.y
      }px)`;
    }
  }
};
</script>

<style lang="scss" scoped>
.base-popover {
  position: relative;
  z-index: 50;

  &__content {
    display: flex;
    flex-direction: column;
  }

  &__overlay {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 40;
    width: 100%;
    height: 100vh;
  }
}
</style>
