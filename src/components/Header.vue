<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <router-link to="/" class="navbar-brand">Stock Trader</router-link>

    <div class="collapse navbar-collapse">
      <ul class="navbar-nav mr-auto">
        <router-link to="/portfolio" class="nav-item" activeClass="active" tag="li">
          <a class="nav-link">Portfolio</a>
        </router-link>
        <router-link to="/stocks" class="nav-item" activeClass="active" tag="li">
          <a class="nav-link">Stocks</a>
        </router-link>
      </ul>
      <ul class="navbar-nav">
        <li class="nav-item active">
          <button class="nav-link btn btn-link" @click="endDay">
            End Day
            <span class="sr-only">(current)</span>
          </button>
        </li>
        <li
          class="nav-item dropdown"
          @click="isDropdownOpen = !isDropdownOpen"
        >
          <a
            class="nav-link dropdown-toggle"
            href="#"
            id="navbarDropdown"
            role="button"
            data-toggle="dropdown"
            aria-haspopup="true"
            aria-expanded="false"
          >Save &amp; Load</a>
          <div class="dropdown-menu" aria-labelledby="navbarDropdown" :class="{show: isDropdownOpen}">
            <a class="dropdown-item" @click="saveData" href="#">Save Data</a>
            <a class="dropdown-item" @click="loadData" href="#">Load Data</a>
          </div>
        </li>
      </ul>
      <strong class="navbar-text ml-3">Funds: {{funds | currency}}</strong>
    </div>
  </nav>
</template>

<script>
import { mapActions } from "vuex";

export default {
  data() {
    return {
      isDropdownOpen: false
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    }
  },
  methods: {
    ...mapActions(["randomizeStocks"]),
    endDay() {
      this.randomizeStocks();
    },
    saveData() {
      const data = {};
    },
    loadData() {}
  }
};
</script>