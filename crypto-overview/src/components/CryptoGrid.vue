<template>
  <h2>Highest marketcap</h2>
    <ul v-if="items" class="crypto-grid">
      <CryptoCard v-for="item in items" :key="item.id" :crypto="item" :newPrice="prices[item.id]" />
    </ul>
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
  }
}
</script>

<style scoped>
.crypto-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 20px;
  list-style: none;
  padding: 0;
}
/* From desktop */
@media (min-width: 979px) {
  .crypto-grid {
    grid-template-columns: repeat(4, 1fr);
  }
}
</style>