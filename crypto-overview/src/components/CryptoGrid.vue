<template>
  <section class="crypto-grid">
    <h1>See all crypto</h1>
    <ul>
      <CryptoCard name="Bitcoin" />
    </ul>
  </section>
</template>

<script>
import CryptoCard from './CryptoCard'

export default {
  name: 'CryptoGrid',
  props: {
    msg: String
  },
  components: {
    CryptoCard
  }
}
</script>
