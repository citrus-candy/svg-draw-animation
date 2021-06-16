<template>
  <component :is="svg" />
</template>

<script>
export default {
  name: "SVGElement",
  props: {
    name: {
      type: String
    }
  },
  computed: {
    svg() {
      return () => import(`@/assets/svg/${this.name}.svg`);
    }
  },
  updated: function() {
    this.$anime({
      targets: "path",
      strokeDashoffset: [this.$anime.setDashoffset, 0],
      easing: "easeInOutSine",
      duration: 500,
      delay: function(el, i) {
        return i * 250;
      }
    });
  }
};
</script>
