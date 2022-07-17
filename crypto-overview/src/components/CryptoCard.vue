<template>
  <li class="crypto-card" v-if="type !== 'list'">
    <span class="crypto-card__name">
      <strong>
        {{crypto.name}}
      </strong>
    </span>
    <span>
      <ArrowDown :up="higher" />
      &dollar;&nbsp;{{price}}
    </span>
    <span :class="(Number(crypto.changePercent24Hr) > 0) ? 'green' : 'red'">
      {{Number(crypto.changePercent24Hr).toFixed(2)}}&nbsp;&percnt;
    </span>
  </li>
  <tr class="crypto-card" v-if="type === 'list'">
    <td>
      {{crypto.name}}
    </td>
    <td>
      <ArrowDown :up="higher" />
      &dollar;&nbsp;{{price}}
    </td>
    <td :class="(Number(crypto.changePercent24Hr) > 0) ? 'green' : 'red'">
      {{Number(crypto.changePercent24Hr).toFixed(2)}}&nbsp;&percnt;
    </td>
  </tr>
</template>

<script>
import ArrowDown from "./icons/ArrowDown";

export default {
  name: 'CryptoCard',
  components: {
    ArrowDown
  },
  props: {
    crypto: Object,
    newPrice: String,
    type: String
  },
  data() {
    return {
      price: this.crypto.priceUsd,
      higher: null
    }
  },
  watch: {
    newPrice(newValue) {
      if (newValue) {
        this.higher = newValue > this.price;
        this.price = newValue
      }
    }
  }
}

</script>

<style scoped lang="scss">
.crypto-card {
  padding: 20px;
  border-radius: 5px;
  background: var(--white-color);
  box-shadow: 0 4px 8px 0 rgba(0,0,0,0.2);

  &__name {
    color: var(--primary-color);
  }

  svg {
    margin-right: 5px;
  }

  span {
    display: block;
    &:not(:last-of-type) {
      margin-bottom: 10px;
    }
    &:last-of-type {
      text-align: right;
    }
  }

  span, td {
    &.green {
      color: green;
    }
    &.red {
      color: red;
    }
  }
}
</style>
