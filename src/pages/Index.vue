<template>
  <Layout>
    <section ref="starField" class="space">
      <div class="stars stars--top">
        <Star v-for="star in 80" :key="star" />
      </div>
      <div class="stars stars--middle">
        <Star v-for="star in 25" :key="star" />
      </div>
      <div class="stars stars--bottom">
        <Star v-for="star in 5" :key="star" />
      </div>
    </section>
  </Layout>
</template>
<script>
import Star from "../components/Star";
export default {
  components: { Star },

  created() {
    window.addEventListener("resize", this.resizeHandler);
  },

  destroyed() {
    window.removeEventListener("resize", this.resizeHandler);
  },

  mounted() {
    this.generateStarField();
  },

  methods: {
    resizeHandler(e) {
      this.generateStarField();
    },

    /**
     * Randomizes position and size of each star.
     * Stars are grouped in slightly overlapping <div> elements.
     * Each layer is contained by <section>.
     * @param maxSize
     *  maximal size of 1st layer stars.
     *  Each layer has 1px smaller max size.
     *  Minimal size is 1px
     */
    generateStarField(maxSize = 3) {
      const container = this.$refs.starField;

      container.childNodes.forEach((layer, index) => {
        layer.childNodes.forEach((star) => {
          star.style.left = Math.random() * layer.clientWidth + "px";
          star.style.top = Math.random() * layer.clientHeight + "px";

          const minSize = index < 0 ? 1 : maxSize - index;
          const size = Math.floor(Math.random() * minSize) + 1 + "px";
          star.style.width = size;
          star.style.height = size;
        });
      });
    },
  },
};
</script>

<style lang="scss">
.home-links a {
  margin-right: 1rem;
}

.space {
  background-image: linear-gradient(
    to bottom,
    #000000,
    #361f2e,
    #5a3c68,
    #6464b1,
    #0096fe
  );
  flex-grow: 1;
  color: white;
  height: 100%;
}

.stars {
  position: relative;

  &--top {
    height: 100vh;
  }

  &--middle,
  &--bottom {
    margin-top: -10vh;
    height: 60vh;
  }
}
</style>
