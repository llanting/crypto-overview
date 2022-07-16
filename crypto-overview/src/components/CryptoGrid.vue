<template>
  <section class="crypto-grid">
    <h1>See all crypto</h1>
    {{prices}}
    <p v-if="!items">Loading...</p>
    <ul v-if="items">
      <CryptoCard v-for="item in items" :key="item.id" :crypto="item" :newPrice="prices[item.id]" />
    </ul>
  </section>
</template>

<script>
import CryptoCard from './CryptoCard'

export default {
  name: 'CryptoGrid',
  props: {
    items: Array,
    prices: Object
  },
  components: {
    CryptoCard
  },
  mounted() {
    console.log(this.prices.bitcoin);
  }
}
</script>
