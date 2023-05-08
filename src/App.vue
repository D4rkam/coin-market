<template>
  <div class="container">
    <div class="row my-3">
      <h1 class="text-center fw-bold">MERCADO DE MONEDAS</h1>
      <input type="text"
        class="form-control bg-dark text-light rounded-0 border-0 my-4"
        placeholder="Buscar Moneda"
        @keyup="searchCoinChildreen()"
        v-model="textSearch"
      >
      <table-coin v-bind:data="data" ref="tableCoin"/>
    </div>
  </div>
</template>

<script>
import TableCoin from '@/components/TableCoin.vue'
export default {
  components: { TableCoin },
  name: "App",
  data(){
    return{
      data: [],
      textSearch: "",
    }
  },
  async mounted() {
    const res = await fetch(
      "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false",
      {
        method: "GET",
        headers: {
          accept: "application/json",
        },
      }
    );
    this.data = await res.json();
  },
  methods: {
    searchCoinChildreen(){
      this.$refs.tableCoin.searchCoin(this.textSearch)
    }
  },
};
</script>

<style>
</style>
