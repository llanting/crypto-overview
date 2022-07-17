<template>
  <h1>Crypto overview</h1>
  <p v-if="!cryptoItems">Loading...</p>
  <!--  First four items-->
  <CryptoGrid v-if="cryptoItems" :items="[...cryptoItems].splice(0, 4)" :prices="cryptoPrices" />
  <!-- Rest of the list -->
  <CryptoList v-if="cryptoItems" :items="[...cryptoItems].splice(4).sort(sortAlphabetically)" :prices="cryptoPrices" />
</template>

<script>
import CryptoGrid from './components/CryptoGrid.vue'
import CryptoList from "@/components/CryptoList";

export default {
  name: 'App',
  components: {
    CryptoGrid,
    CryptoList
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
      const pricesWs = new WebSocket(`${process.env.VUE_APP_WEBSOCKET_URL}/prices?assets=${this.cryptoIds.join(",")}`)

      pricesWs.onmessage = (msg) => {
        this.cryptoPrices = JSON.parse(msg.data);
      }
    },
    sortAlphabetically(a, b) {
      if (a.id < b.id) {
        return -1;
      }
      if (a.id > b.id) {
        return 1;
      }
      return 0;
    }
  },

  mounted() {
    this.fetchData()
  },
}
</script>

<style>
@import "../assets/styles/variables.css";
@import "../assets/styles/global.css";

</style>
