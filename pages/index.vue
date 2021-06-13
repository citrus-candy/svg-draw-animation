<template>
  <div class="container">
    <div>
      <input type="text" v-model="text" />
      <button @click="draw">Draw</button>
      <button @click="animation">Animaton</button>
      <button @click="reset">Reset</button>
    </div>
    <div class="text_field">
      <div class="svg" v-for="svgpath in svgpaths" :key="svgpath.key">
        <SVGElement v-show="svgpath != '' && btnFlag" :name="svgpath" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: () => ({ texts: [], text: "", svgpaths: [], btnFlag: false }),
  methods: {
    animation() {
      this.btnFlag = true;
      this.$anime({
        targets: "svg path",
        strokeDashoffset: [this.$anime.setDashoffset, 0],
        easing: "easeInOutSine",
        duration: 500,
        delay: function(el, i) {
          return i * 250;
        }
      });
      console.log("text");
    },
    draw() {
      this.texts = [];
      this.svgpaths = [];
      this.texts = this.text.split("");
      this.texts.forEach(e => {
        this.svgpaths.push(("000" + e.charCodeAt(0).toString(16)).slice(-5));
      });
      console.log(this.svgpaths);
    },
    reset() {
      this.texts = [];
      this.text = "";
      this.svgpaths = [];
      this.btnFlag = false;
    }
  },
  watch: {
    btnFlag() {
      if (this.btnFlag) {
        console.log(this.svgpaths);
        this.$anime({
          targets: "svg path",
          strokeDashoffset: [this.$anime.setDashoffset, 0],
          easing: "easeInOutSine",
          duration: 500,
          delay: function(el, i) {
            return i * 250;
          }
        });
      }
    }
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  flex-direction: column;
}

.text_field {
  display: flex;
  width: 60vw;
  flex-wrap: wrap;
  justify-content: center;
  border: solid 2px;
  margin-top: 40px;
}
</style>
