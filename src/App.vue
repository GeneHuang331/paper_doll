<script setup></script>
<template>
  <main>
    <div class="img__container">
      <img :src="catSrc" alt="品種" />
    </div>
    <div class="button__container">
      <button @click="reShake()">GO</button>
    </div>
  </main>
</template>
<script>
export default {
  data() {
    return {
      catNum: 0,
      timeOut: 17,
      timer: null,
    };
  },
  methods: {
    shake() {
      console.log(this.catNum, this.timeOut);
      if (this.timeOut < 600) {
        this.getRandom(1, 5);
        this.timeOut *= 1.2;
        this.timer = setTimeout(this.shake, this.timeOut);
      } else {
        clearTimeout(this.timer);
      }
    },
    reShake() {
      this.timeOut = 17;
      this.shake();
    },
    getRandom(min, max) {
      this.catNum = Math.round(min + Math.random() * (max - min));
    },
  },
  computed: {
    catSrc() {
      return new URL(`./assets/img/breed_${this.catNum}_b.png`, import.meta.url)
        .href;
    },
  },
  mounted() {
    this.shake();
  },
};
</script>
<style scoped lang="scss">
.img__container {
  text-align: center;
}
.button__container {
  text-align: center;
}
</style>
