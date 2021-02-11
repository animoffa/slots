<template>
  <div name="homeTab">
    <div class="slider" ref="slider">
      <div class="slider__track" ref="slider__truck">
        <div
          class="slider__slide slide"
          :style="{ background: slide.background }"
          v-for="(slide, i) of slides"
          :key="i"
        >
          <div class="slide__text">
            <p class="slide__title">{{ slide.title }}</p>
          </div>
        </div>
      </div>
      <div class="slider__buttons">
        <button class="btn btn_prev" :disabled="position === 0" @click="prev">
          prev
        </button>
        <button
          class="btn btn_next"
          :disabled="currentSlide === slides.length"
          @click="next"
        >
          next
        </button>
      </div>
    </div>
  </div>
</template>
<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data() {
    return {
      slides: [
        {
          title: "Directed",
          background: "red",
        },
        {
          title: "By ",
          background: "green",
        },
        {
          title: "Robert B. Weide",
          background: "yellow",
        },
      ],
      position: 0 as number,
      currentSlide: 1 as number,
    };
  },
  methods: {
    next() {
      if (this.currentSlide < this.slides.length) {
        this.currentSlide += 1;
        const itemWidth = (this.$refs.slider as HTMLElement).clientWidth;
        const itemsLeft =
          this.slides.length -
          (Math.abs(this.position) + itemWidth) / itemWidth;
        this.position -= itemsLeft >= 1 ? itemWidth : itemsLeft * itemWidth;
        this.setPosition();
      }
    },
    prev() {
      if (this.currentSlide > 1) {
        this.currentSlide -= 1;
        const itemWidth = (this.$refs.slider as HTMLElement).clientWidth;
        const itemsLeft = Math.abs(this.position) / itemWidth;
        this.position += itemsLeft >= 1 ? itemWidth : itemsLeft * itemWidth;
        this.setPosition();
      }
    },
    setPosition() {
      (this.$refs
        .slider__truck as HTMLElement).style.transform = `translateX(${this.position}px)`;
    },
  },
});
</script>

<style scoped>
.slider {
  overflow: hidden;
  width: 15rem;
  height: 120px;
}

.slider__track {
  display: flex;
  transition: 0.5s;
}
.slider__slide {
  min-width: 15rem;
  height: 30px;
}
.buttons {
  margin-top: 20px;
}
</style>