<template>
  <div class="col-sm-6 col-md-4">
    <div class="card" >
      <div class="card-header bg-info">
        <h3 class="panel-title">
          {{stock.name}}
          <small>(Price: {{stock.price}}  |  Quantity: {{stock.quantity}})</small>
        </h3>
      </div>
      <div class="card-body">
        <div class="row">
          <div class="col">
            <input type="number" class="form-control" placeholder="Quantity" v-model="quantity">
          </div>
          <div class="col">
            <button class="btn btn-success" @click="sellStock" :disabled=" quantity <= 0 || !Number.isInteger(quantity)">Sell</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import {mapActions} from 'vuex'

export default {
  props:['stock'],
  data() {
    return {
      quantity: 0
    }
  },
  methods: {
        ...mapActions({
            placeSellOrder: 'sellStock'
        }),
      sellStock(){
            const order = {
            stockId: this.stock.id,
            stockPrice: this.stock.price,
            quantity: this.quantity
            }
            this.placeSellOrder(order)
            this.quantity = 0
        }
  },
}
</script>