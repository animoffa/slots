<template>
  <div>
    <button
      class="tab"
      v-for="(tab, i) in tabs"
      :key="i"
      :class="['tab-button', { active: currentTab === tab }]"
      @click="changeTab(tab)"
    >
      <div class="tab__content">
        <span> {{ tab }} </span>
        <transition name="slide-fade">
          <div class="tab__close" @click="deleteTab(i)">x</div>
        </transition>
      </div>
    </button>
  </div>
</template>
<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  data() {
    return {};
  },
  props: {
    currentTab: {
      type: String,
      default: ["home"],
    },
    tabs: {
      type: Array,
      required: true,
      default: ["home", "about"],
    },
  },
  methods: {
    changeTab(tab: string) {
      this.$emit("change-tab", tab);
    },
    deleteTab(i: string) {
      this.$emit("delete-tab", i);
    },
  },
});
</script>
<style scoped>
.slide-fade-enter-active {
  transition: all 0.3s ease;
}
.slide-fade-leave-active {
  transition: all 0.8s cubic-bezier(1, 0.5, 0.8, 1);
}
.slide-fade-enter, .slide-fade-leave-to
/* .slide-fade-leave-active до версии 2.1.8 */ {
  transform: translateX(10px);
  opacity: 0;
}
.tab__close {
  background: red;
  color: white;
  width: 18px;
  height: 18px;
  font-size: 20px;
  color: white;
  border-radius: 50%;
  font-size: 14px;
  padding-bottom: 3px;
  display: none;
  align-items: center;
  justify-content: center;
}
.active .tab__close {
  display: flex;
}
.tab__content {
  display: flex;
  justify-content: space-around;
}
</style>