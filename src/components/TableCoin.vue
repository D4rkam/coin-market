<template>
  <table class="table table-dark">
    <thead>
      <tr>
        <th v-for="title in titles" :key="title" class="text-center">
          {{ title }}
        </th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(coin, index) in filteredCoins" :key="coin.id">
        <td class="text-muted text-center">
          {{ index + 1 }}
        </td>

        <td>
          <img :src="coin.image" style="width: 2rem" class="me-2" />
          <span>{{ coin.name }}</span>
          <span class="ms-2 text-uppercase text-muted">{{ coin.symbol }}</span>
        </td>

        <td class="text-center">
          <span>${{ coin.current_price.toLocaleString() }}</span>
        </td>

        <td class="text-center">
          <span
            :class="[
              coin.price_change_percentage_24h > 0
                ? 'text-success'
                : 'text-danger',
            ]"
          >
            {{ coin.price_change_percentage_24h }} %
          </span>
        </td>

        <td class="text-center">
          <span> ${{ coin.total_volume.toLocaleString() }} </span>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: "TableCoin",
  props: {
    data: Array,
  },
  data() {
    return {
      coins: this.data,
      filteredCoins: this.data,
      titles: ["#", "Coin", "Price", "Price Change", "24h Volume"],
    };
  },

  methods: {
    searchCoin(textSearch) {
      this.filteredCoins = this.coins.filter(
        (coin) =>
          coin.name.toLowerCase().includes(textSearch.toLowerCase()) ||
          coin.symbol.toLowerCase().includes(textSearch.toLowerCase())
      );
    },
  },
};
</script>