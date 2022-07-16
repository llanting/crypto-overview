<template>
  <CryptoGrid :items="cryptoItems" />
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
      cryptoItems: null
    };
  },

  methods: {
    async fetchData() {
      this.cryptoItems = null
      const res = await fetch(
          process.env.VUE_APP_API_URL, {
            headers: new Headers({
              "Accept-Encoding": "gzip"
            })
          }
      )
      const result = await res.json();
      this.cryptoItems = await result.data;
    }
  },

  mounted() {
    this.fetchData()
  }
}
</script>
