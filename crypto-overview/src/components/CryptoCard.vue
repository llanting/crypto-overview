<template>
  <li class="crypto-card">
    {{crypto.name}}
  </li>
</template>

<script>
export default {
  name: 'CryptoCard',
  props: {
    crypto: Object
  }
}
</script>
