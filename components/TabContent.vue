<template>
  <div class="tab-container">
    <h3 class="title">
      {{ tabName }}
    </h3>
    <slot></slot>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
export default Vue.extend({
  props: {
    tabName: {
      type: String,
      required: true,
    },
  },
});
</script>
<style scoped>
.tab-container{
    min-width: 15.4%;
}
</style>