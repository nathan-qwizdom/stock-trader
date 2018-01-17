<template>
  <div>
    <p>Your funds: {{ funds | currency }}</p>
  </div>
</template>

<script>
  export default {
    computed: {
      funds(){
        return this.$store.getters.funds;
      }
    }
  }
</script>
