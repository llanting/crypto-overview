<template>
  <section class="crypto-grid">
    <h1>See all crypto</h1>
    {{prices}}
    <p v-if="!items">Loading...</p>
    <ul v-if="items">
      <CryptoCard v-for="item in items" :key="item.id" :crypto="item" />
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
  }
}
</script>
