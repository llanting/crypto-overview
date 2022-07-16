<template>
  <li class="crypto-card">
    {{crypto.id}}
    {{crypto.priceUsd}}
  </li>
</template>

<script>
export default {
  name: 'CryptoCard',
  props: {
    crypto: Object
  },
}

</script>
