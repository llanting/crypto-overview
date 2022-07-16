<template>
  <li class="crypto-card">
    {{crypto.id}}
    <div>
    {{price}}
    </div>
    <div v-if="crypto.changePercent24Hr > 0">Up</div>
    <div v-if="crypto.changePercent24Hr < 0">Down</div>
    {{crypto.changePercent24Hr}}
  </li>
</template>

<script>
export default {
  name: 'CryptoCard',
  props: {
    crypto: Object,
    newPrice: String
  },
  data() {
    return {
      price: this.crypto.priceUsd
    }
  },
  watch: {
    newPrice(newValue) {
      if (newValue) {
        this.price = newValue
      }
    }
  }
}

</script>
