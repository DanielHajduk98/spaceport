<template>
  <Layout>
    <section id="space">
      <div ref="starField">
        <div class="stars stars--top">
          <Star v-for="star in 80" :key="star" />
        </div>
        <div class="stars stars--middle">
          <Star v-for="star in 25" :key="star" />
        </div>
        <div class="stars stars--bottom">
          <Star v-for="star in 5" :key="star" />
        </div>
      </div>
      <div class="spaceStation-wrapper">
        <div class="container center">
          <button @click="scrollToEarth">Scroll bottom</button>
        </div>
      </div>
    </section>

    <section id="earth">
      <div class="rocket-wrapper-outer">
        <div id="rocket" class="rocket-wrapper-inner">
          <button @click="scrollToSpace" class="rocket">scroll to top</button>
        </div>
      </div>
    </section>
  </Layout>
</template>

<script>
// TODO ruler on one side as navigation with different layers eg. stratosphere
// TODO curved earth
// TODO svg editor to create space station, plane and rocket, clouds
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

    scrollToEarth() {
      this.$scrollTo("#rocket", 4000, { easing: "ease-in-out" });
    },

    scrollToSpace() {
      this.$scrollTo("#space", 4000, { easing: "ease-in-out" });
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
#space {
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
  position: relative;
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

.spaceStation-wrapper {
  position: absolute;
  top: calc(100vh - 100px);
  left: 0;
  width: 100%;
}

#earth {
  position: relative;
  margin-top: -20px;
  min-height: 100vh;
  background: saddlebrown;
  border-radius: 55% 55% 0% 0% / 5px 5px 0% 0%;
}

.rocket-wrapper {
  &-outer {
    display: flex;
    justify-content: center;
    align-content: center;
    padding: 0;
    height: 0;
    position: relative;
  }

  &-inner {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    display: flex;
    justify-content: center;
    align-content: center;
    z-index: 100;
  }
}

.rocket {
  height: 200px;
}
</style>
