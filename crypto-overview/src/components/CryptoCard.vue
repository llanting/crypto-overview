<template>
  <li class="crypto-card">
    {{name}}
  </li>
</template>

<script>
export default {
  name: 'CryptoCard',
  props: {
    name: String
  }
}
</script>
