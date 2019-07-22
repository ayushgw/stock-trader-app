<template>
  <div class="d-flex flex-wrap p-4">
    <app-stock v-for="(stock, index) in stocks" :key="index" :stock="stock"></app-stock>
  </div>
</template>

<script>
import Stock from './Stock.vue';

export default {
  data() {
    return {
      stocks: [
        { id: 1, name: "BMW", price: 100 },
        { id: 2, name: "Google", price: 190 },
        { id: 3, name: "Twitter", price: 200 },
        { id: 4, name: "OpIndia", price: 500 }
      ]
    };
  },
  components: {
      appStock: Stock
  }
};
</script>