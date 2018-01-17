<template>
  <div>
    <h1 class="is-size-5 has-text-weight-bold has-text-centered">Hello, Welcome to the Stock Trader App.</h1>
    <div>
      <p class="has-text-centered">Your stocks will appear here when purchased.</p>
    </div>
    <app-stock v-for="stock in stocks" :stock="stock"></app-stock>
  </div>
</template>
<script>
  import {mapGetters} from 'vuex';
  import Stock from './Stock.vue';
  export default{
    computed: {
      ...mapGetters({
        stocks: 'stockPortfolio'
      })
    },
    components: {
      appStock: Stock
    }
  }
</script>
