<template>
  <div class="col-sm-6 col-md-4 my-2">
    <div class="card">
      <h5 class="card-header bg-info">
        {{stock.name}}
        <small>(Price: {{stock.price}} | Quantity: {{stock.quantity}})</small>
      </h5>
      <div class="card-body">
        <div class="d-flex">
          <div class="w-50">
            <input
              type="number"
              class="form-control"
              placeholder="Quantity"
              v-model.number="quantity"
              :class="{'border border-danger shadow-none': insufficientQuantity}"
            />
          </div>
          <div class="mx-2 flex-fill text-right">
            <button
              class="btn btn-success"
              @click="sellStock"
              :disabled="insufficientQuantity || quantity <= 0 || !Number.isInteger(quantity)"
            >{{ insufficientQuantity ? 'Unavailable' : 'Sell'}}</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapActions } from "vuex";

export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0
    };
  },
  computed: {
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    }
  },
  methods: {
    ...mapActions({
      placeSellOrder: "sellStock"
    }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        stockQuantity: this.quantity
      };
      this.placeSellOrder(order);
      this.quantity = 0;
    }
  }
};
</script>