<template>
  <div class="navbar has-shadow is-dark">
    <div class="container">
      <div class="navbar-brand">
        <router-link to="/" class="navbar-item r-item has-text-weight-bold is-size-5">stock trader</router-link>
        <span class="navbar-burger" @click="toggleNav" :class="{ 'is-active': isActive }">
            <span></span>
            <span></span>
            <span></span>
        </span>
      </div>
      <div class="navbar-menu" v-bind:class="{ 'is-active': isActive }">
        <div class="navbar-start">
          <router-link to="/" class="navbar-item r-item">Portfolio</router-link>
          <router-link to="/stocks" class="navbar-item r-item">Stocks</router-link>
        </div>
        <div class="navbar-end">
          <strong class="navbar-item">Funds: {{ funds | currency }}</strong>
          <a class="navbar-item" @click="endDay">End Day</a>
          <div
            class="navbar-item has-dropdown"
            :class="{'is-active': dropdownOpen}"
            @click="dropdownOpen = !dropdownOpen">
              <a class="navbar-link">Save & Load</a>
              <div class="navbar-dropdown is-right">
                <a class="navbar-item" @click="saveData">Save Data</a>
                <a class="navbar-item" @click="loadData">Load Data</a>
              </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import{mapActions} from 'vuex';

export default {
  computed: {
    funds(){
        return this.$store.getters.funds;
    }
  },
  data() {
    return {
      isActive: false,
      dropdownOpen: false
    }
  },
  methods: {
    toggleNav() {
      this.isActive = !this.isActive;
    },
    ...mapActions({
        randomizeStocks: 'randomizeStocks',
        fetchData: 'loadData'
    }),
    endDay(){
      this.randomizeStocks();
    },
    saveData(){
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks
      };
      this.$http.put('data.json', data);
    },
    loadData(){
      this.fetchData();
    }
  }
}
</script>
