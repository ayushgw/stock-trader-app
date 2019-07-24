<template>
  <div>
    <app-header></app-header>
    <div class="row">
      <div class="col-12">
        <transition
          name="custom-classes-transition"
          enter-active-class="animated fadeIn"
          leave-active-class="animated slideOutLeft"
          mode="out-in"
          :duration="{ enter: 300, leave: 200 }"
        >
          <router-view></router-view>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
export default {
  components: {
    appHeader: Header
  },
  created() {
    this.$store.dispatch("initStocks");
  }
};
</script>

<style>
body {
  padding: 30px 120px;
}
</style>
