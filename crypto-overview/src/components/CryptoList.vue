<template>
  <h2>Andere waarden</h2>
  <table v-if="items" class="crypto-list">
    <thead>
    <tr>
      <th>Naam</th>
      <th>Koers</th>
      <th>Winst/verlies</th>
    </tr>
    </thead>
    <tbody>
      <CryptoCard v-for="item in items" :key="item.id" :crypto="item" :newPrice="prices[item.id]" type="list" />
    </tbody>
  </table>
</template>

<script>

import CryptoCard from "@/components/CryptoCard";

export default {
  name: 'CryptoList',
  props: {
    items: Array,
    prices: Object
  },
  components: {
    CryptoCard
  },

}
</script>

<style scoped lang="scss">
.crypto-list {
  list-style: none;
  padding: 0;
  width: 100%;
  border-collapse: collapse;

  thead {
    font-weight: 700;
    th {
      padding-bottom: 10px;
      text-align: left;
      color: var(--primary-color);
      &:last-of-type {
        text-align: right;
      }
    }
  }

  :deep(.crypto-card) {
    &:not(:last-of-type) {
      td {
        border-bottom: 1px solid rgba(0, 0, 0, 0.2);
      }
    }
    td {
      padding: 10px 5px;
      &:last-of-type {
        text-align: right;
      }
    }
  }
}
</style>
