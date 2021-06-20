<template>
  <div class="container">
    <SVGAnimation ref="svgAnim" :text="text" />
    <div class="input_form">
      <textarea type="text" v-model="text" />
      <div class="button_field">
        <!-- <button @click="draw()">Draw</button> -->
        <button @click="reset()">Reset</button>
      </div>
    </div>
  </div>
</template>

<script>
import SVGAnimation from "../components/SVGAnimation.vue";

export default {
  components: { SVGAnimation },
  data: () => ({
    text: ""
  }),
  methods: {
    draw() {
      this.$refs.svgAnim.draw();
    },
    reset() {
      this.text = "";
      this.$refs.svgAnim.reset();
    }
  }
};
</script>

<style scoped>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  flex-direction: column;
}

textarea {
  width: 300px;
  height: 100px;
}
.input_form {
  padding-top: 20px;
}
</style>
