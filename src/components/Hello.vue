<template>
  <div class="hello">
    <h1>CryptoCompare API Results</h1>
    <div id="crypto-container" v-for="(value, key) in cryptos" v-bind:key="key">
      <span class="left">{{ key }}</span>
      <span class="right">${{ value.USD }}</span>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "hello",
  data: () => ({
    cryptos: [],
    errors: []
  }),

  created() {
    const fsymsList =
      "BTC,XRP,BCH,ETH,ZEC,EOS,XMR,ETC,LTC,DASH,QTUM,NEO,XLM,TRX,ADA,BTS,USDT,XUC,PAX,IOT";

    axios
      .get(
        "https://min-api.cryptocompare.com/data/pricemulti?fsyms=" +
          fsymsList +
          "&tsyms=USD"
      )
      .then(response => {
        this.cryptos = response.data;
      })
      .catch(error => {
        this.errors.push(error);
      });
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
body {
  background: #f1f1f1;
}

div#crypto-container {
  background: white;
  width: 70%;
  margin: 0 auto 4px auto;
  padding: 1em;
  box-shadow: 1px 1px 0 lightgrey;
}

span.left {
  float: left;
  font-weight: bold;
}

span.right {
  float: right;
}
</style>
