<template>
<div class="column is-one-third">
  <div class="card">
    <header class="card-header" style="justify-content: center;">
      <div class="content">
        <p class="card-header-title" style="padding-bottom: 0; margin-bottom: 0; justify-content: center;">
          {{ stock.name }}
        </p>
        <span class="is-size-6" style="display: block; margin-bottom: 12px; text-align: center;">Price: £{{ stock.price }}</span>
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
            :class="{'is-danger': insufficientFunds}">
        </div>
        <div class="control">
          <button
            class="button is-primary"
            @click="buyStock"
            :disabled="insufficientFunds || quantity <= 0">
            {{ insufficientFunds ? 'Insufficient Funds' : 'Buy' }}
          </button>
        </div>
      </div>
    </div>
  </div>
</div>
</template>

<script>
  export default{
    props: ['stock'],
    data(){
      return{
        quantity: 0
      }
    },
    computed: {
      funds(){
        return this.$store.getters.funds;
      },
      insufficientFunds(){
        return this.quantity * this.stock.price > this.funds;
      }
    },
    methods: {
      buyStock(){
        const order = {
          stockId: this.stock.id,
          stockPrice: this.stock.price,
          quantity: this.quantity
        };
        this.$store.dispatch('buyStock', order);
        this.quantity = 0;
      }
    }
  }
</script>
