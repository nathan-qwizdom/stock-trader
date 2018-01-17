<template>
<div class="app-container">
  <app-header></app-header>
  <section class="section">
    <div class="columns">
      <div class="column">
        <transition name="slide" mode="out-in">
          <router-view></router-view>
        </transition>
      </div>
    </div>
  </section>
</div>
</template>

<script>
import Header from './components/Header.vue'
export default {
  data() {
    return {

    }
  },
  components: {
    AppHeader: Header
  },
  created(){
    this.$store.dispatch('initStocks');
  }
}
</script>

<style>
.app-container > .section{
  padding: 30px 15px;
  max-width: 1200px;
  margin: auto;
}

.slide-enter-active{
  animation: slide-in 400ms ease-out forwards;
}

.slide-leave-active{
  animation: slide-out 400ms ease-out forwards;
}

@keyframes slide-in{
  from{
    transform: translateX(-60px);
    opacity: 0;
  }
  to{
    transform: translateX(0px);
    opacity: 1;
  }
}

@keyframes slide-out{
  from{
    transform: translateX(0px);
    opacity: 1;
  }
  to{
    transform: translateX(-60px);
    opacity: 0;
  }
}
</style>
