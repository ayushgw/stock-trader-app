<template>
  <div class="col-sm-6 col-md-4 my-2">
    <div class="card">
      <h5 class="card-header">
        {{stock.name}}
        <small>(Price: {{stock.price}})</small>
      </h5>
      <div class="card-body">
        <div class="d-flex">
          <input type="number" class="form-control" placeholder="Quantity" v-model.number="quantity" />
          <div class="mx-2">
            <button class="btn btn-success" @click="buyStock" :disabled="quantity <= 0 || !Number.isInteger(quantity)">Buy</button>
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
        }
    },
    methods: {
        buyStock() {
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                stockQuantity: this.quantity
            };
            console.log(order);
            this.quantity = 0;
        }
    }
}
</script>