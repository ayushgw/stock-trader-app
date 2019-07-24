<template>
  <div class="col-sm-6 col-md-4 my-2">
    <div class="card">
      <h5 class="card-header">
        {{stock.name}}
        <small>(Price: {{stock.price}})</small>
      </h5>
      <div class="card-body">
        <div class="d-flex">
          <div class="w-50">
            <input
              type="number"
              class="form-control"
              placeholder="Quantity"
              v-model.number="quantity"
              :class="{'border border-danger shadow-none' : insufficientFunds}"
            />
          </div>
          <div class="mx-2 flex-fill text-right">
            <button
              class="btn btn-success"
              @click="buyStock"
              :disabled="insufficientFunds || quantity <= 0 || !Number.isInteger(quantity)"
            >{{ insufficientFunds ? 'Low Funds' : 'Buy'}}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    insufficientFunds() {
      return this.quantity * this.stock.price >= this.funds;
    }
  },
  methods: {
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        stockQuantity: this.quantity
      };
      this.$store.dispatch("buyStock", order);
      this.quantity = 0;
    }
  }
};
</script>