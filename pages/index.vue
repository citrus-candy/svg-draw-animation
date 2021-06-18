<template>
  <div class="container">
    <div>
      <input type="text" v-model="text" />
      <button @click="draw">Draw</button>
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
    draw() {
      this.texts = [];
      this.svgpaths = [];
      this.texts = this.text.split("");
      this.texts.forEach(e => {
        this.svgpaths.push(("000" + e.charCodeAt(0).toString(16)).slice(-5));
      });
      console.log("svgpaths:[" + this.svgpaths + "]");
      this.btnFlag = true;
    },
    reset() {
      this.texts = [];
      this.text = "";
      this.svgpaths = [];
      this.btnFlag = false;
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
  justify-content: flex-start;
  margin-top: 40px;
}
</style>
