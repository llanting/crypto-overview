<template>
  <CryptoGrid :items="cryptoItems" :prices="cryptoPrices" />
</template>

<script>
import CryptoGrid from './components/CryptoGrid.vue'

export default {
  name: 'App',
  components: {
    CryptoGrid
  },
  data() {
    return {
      cryptoItems: [],
      cryptoIds: [],
      cryptoPrices: {}
    };
  },

  methods: {
    async fetchData() {
      this.cryptoItems = null
      const res = await fetch(
          `${process.env.VUE_APP_API_URL}/assets?limit=50`, {
            headers: new Headers({
              "Accept-Encoding": "gzip"
            })
          }
      )
      const result = await res.json();
      this.cryptoItems = await result.data;
      this.cryptoItems.forEach(({id}) => {
        this.cryptoIds.push(id);
      })
      this.connectToWebSocket()
    },
    connectToWebSocket() {
      const pricesWs = new WebSocket(`wss://ws.coincap.io/prices?assets=${this.cryptoIds.join(",")}`)

      pricesWs.onmessage = (msg) => {
        this.cryptoPrices = JSON.parse(msg.data);
      }
    }
  },

  mounted() {
    this.fetchData()
  }
}
</script>
