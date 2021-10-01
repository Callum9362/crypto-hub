<template>
  <div>
      <p v-if="$fetchState.pending">Fetching Exchanges...</p>
      <p v-else-if="$fetchState.error">An error occured</p>
      <div v-else>
          <h6>Top Ten Exchanges</h6>
          <ul>
            <li v-for="exchange of exchanges" :key="exchange.id">{{ exchange.name }}</li>
          </ul>
      </div>
  </div>
</template>

<script>
  export default{
    data(){
      return {
        exchanges:[]
      }
    },
    async fetch()
    {
      this.exchanges = await fetch(
        'https://api.coingecko.com/api/v3/exchanges?per_page=10&page=1'
      ).then(res => res.json())
    }
  }
</script>
