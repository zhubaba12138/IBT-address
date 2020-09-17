<template>
  <div id="app">
    <ul>
      <li v-for="(item, key) in this.adderssList" :key="key">
        <p>{{ item }}</p>
        <p>初始值：{{ old_wallet[item] }}</p>
        <span>当前值：{{ wallet[item] }}</span>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "App",
  data() {
    return {
      adderssList: [
        "TNawcJhC2GrrrrhxdWXPTD8Dcr2848m3KF",
        "TFLvfXzFtDsvPKnS2fc4zv28kowzgEwjh2"
      ],
      old_wallet: {
        TNawcJhC2GrrrrhxdWXPTD8Dcr2848m3KF: 124734,
        TFLvfXzFtDsvPKnS2fc4zv28kowzgEwjh2: 80255
      },
      wallet: {
        TNawcJhC2GrrrrhxdWXPTD8Dcr2848m3KF: 124734,
        TFLvfXzFtDsvPKnS2fc4zv28kowzgEwjh2: 80255
      }
    };
  },
  mounted() {
    let k = 0;
    setInterval(() => {
      axios
        .get(
          `https://apilist.tronscan.org/api/account?address=${this.adderssList[k]}`
        )
        .then(res => {
          let balanceList = res.data.trc20token_balances;
          if (balanceList.length > 0) {
            balanceList.forEach(token => {
              if (
                token.symbol === "IBT" &&
                token.contract_address === "TWSuK6c6h9NrnXZEHLrnu8DHaDv1kNFgf6"
              ) {
                this.wallet[res.data.address] = token.balance.substring(
                  0,
                  token.balance.length - token.decimals
                );
              }
            });
          }
        });
      if (k === this.adderssList.length - 1) {
        k = -1;
      }
      k++;
    }, 2000);
  }
};
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
li {
  list-style: none;
  height: 156px;
  box-shadow: rgba(0, 0, 0, 0.5) 0px 0px 3rem -1rem;
  padding-top: 50px;
  margin-bottom: 20px;
}
</style>
