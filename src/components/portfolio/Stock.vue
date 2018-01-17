<template>
<div class="column is-one-third">
  <div class="card">
    <header class="card-header" style="justify-content: center;">
      <div class="content">
        <p class="card-header-title" style="padding-bottom: 0; margin-bottom: 0; justify-content: center;">
          {{ stock.name }}
        </p>
        <span class="is-size-6" style="display: block; margin-bottom: 12px; text-align: center;">Price: £{{ stock.price }} | {{ stock.quantity }} stocks</span>
      </div>
    </header>
    <div class="card-content">
      <div class="field has-addons" style="justify-content: center;">
        <div class="control">
          <input
            class="input"
            type="number"
            placeholder="Quantity..."
            v-model="quantity"
            :class="{'is-danger': insufficientQuantity}">
        </div>
        <div class="control">
          <button
            class="button is-primary"
            @click="sellStock"
            :disabled="insufficientQuantity || quantity <= 0">
            {{ insufficientQuantity ? 'Not enough stocks' : 'Sell'}}
          </button>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
  import {mapActions} from 'vuex';
  export default{
    props: ['stock'],
    data(){
      return{
        quantity: 0
      }
    },
    computed: {
      insufficientQuantity(){
        return this.quantity > this.stock.quantity;
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
        };
        this.placeSellOrder(order);
        this.quantity = 0;
      }
    }
  }
</script>
