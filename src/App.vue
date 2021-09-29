<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <button v-on:click='login'>login</button>
  <button v-on:click='listAll'>All NFTs</button>
  <button v-on:click='listMine'>My NFTs</button>
  <button v-on:click='buy'>Buy</button>
  <button v-on:click='reveal'>Reveal</button>

  <h2>Price: {{ this.price }}</h2>
</template>

<script>
// eslint-disable-next-line
import api from '@danielwpz/tenk-api'

export default {
  name: 'App',
  components: {
  },
  data: () => {
    return {
      price: '99'
    }
  },
  async mounted () {
    await api.init()
    console.log(api.getAccountId())

    // load price
    this.price = await api.getUnitPrice()
  },
  methods: {
    login () {
      api.signIn()
    },
    async listAll () {
      const nfts = await api.getNFTs(0)
      console.log(nfts)
    },
    async listMine () {
      const nfts = await api.getMyCollections()
      console.log(nfts)
    },
    async buy () {
      const nft = await api.purchase('http://localhost:8082/')
      console.log(nft)
    },
    async reveal () {
      const nft = await api.getSuccessResult()
      console.log(nft)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
