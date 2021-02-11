<template>
  <div class="container">
    <h1 class="add" @click="formIsShow = !formIsShow">
      <template v-if="formIsShow">-</template>
      <template v-else>+</template>
    </h1>
    <transition name="fade">
      <form class="form" v-if="formIsShow" @submit.prevent="onSubmit">
        <input class="form__input" v-model="newTabName" placeholder="tab" />
        <button class="form__button button">add</button>
      </form>
    </transition>
    <Tab
      :tabs="tabs"
      :currentTab="currentTab"
      @change-tab="changeTab"
      @delete-tab="deleteTab"
    />
    <TabContent :tabName="currentTab">
      <transition name="fade">
        <template v-if="setContent()">
          <component v-bind:is="currentTabComponent" class="tab"></component>
        </template>
      </transition>
    </TabContent>
  </div>
</template>

  <script lang="ts">
import Tab from "../components/Tab";
import TabContent from "../components/TabContent";
import HomeTab from "../components/HomeTab";
import PostsTab from "../components/PostsTab";
import Vue from "vue";
export default Vue.extend({
  data() {
    return {
      currentTab: "Home" as string,
      tabs: ["Home", "Posts", "Archive"] as Array<string>,
      tabPages: ["PostsTab", "HomeTab"] as Array<string>,
      formIsShow: false,
      newTabName: "" as string,
    }
  },
  components: {
    HomeTab,
    Tab,
    TabContent,
    PostsTab,
  },
  computed: {
    currentTabComponent(): string {
      return this.currentTab + "Tab";
    },
  },
  methods: {
    changeTab(tab): any {
      this.currentTab = tab;
    },
    setContent(): boolean {
      return this.tabPages.includes(this.currentTabComponent);
    },
    onSubmit() {
      this.$set(this.tabs, this.tabs.length, this.newTabName);
      this.newTabName = "";
    },
    deleteTab(tab) {
      this.tabs.splice(tab, 1);
    },
  },
  head(): any {
    return {
      title: this.currentTab,
    };
  },
});
</script>

<style>
.tab-button {
  padding: 6px 10px;
  border-top-left-radius: 3px;
  border-top-right-radius: 3px;
  border: 1px solid #ccc;
  cursor: pointer;
  background: #f0f0f0;
  margin-bottom: -1px;
  margin-right: -1px;
}
.tab-button:hover {
  background: #e0e0e0;
}
.tab-button.active {
  background: #e0e0e0;
  position: relative;
  top: -1px;
}
.tab {
  border: 1px solid #ccc;
  height: 30px;
  min-width: 100px;
  min-height: 20px;
}
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
  opacity: 0;
}
.container {
  min-width: 100vw;
  display: flex;
  position: relative;
  top: 60px;
  align-items: center;
  flex-direction: column;
}
form {
  display: flex;
  margin-bottom: 20px;
}
.add{
  cursor: pointer;
}
</style>