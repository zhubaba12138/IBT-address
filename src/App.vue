<template>
  <div id="app">
    <ul>
      <li v-for="(item, key) in this.adderssList" :key="key">
        <span>{{ item }}</span>
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
        "TZ7LFhgZtHdPgfetaQioB6RGPHv44K5YSV",
        "TQgAJin7TSHRxMYC67CJ713ct7DQ7hbPRE",
        "TFLQwhip363fMkBATfDPTUYibzy9GmsZYJ",
        "TVgam8pQNJ5sXuwRQye2MuGB4p5Q1MFQvw",
        "TH2SfRrGg1XRuWvQJebvfd9cGdoqARybBF",
        "TXZ4eQ3RQHHDeVNhCCXLEJP5WkynVU9d4T",
        "TQipTdM4cqxDQv7rRoKmGwjfuNdb3mm6Pe",
        "TYZAxWS1RvhL5gamUgDnqvfmKHaa6kZKGh",
        "TX4mNg9Sfmr3gxaKi9tB9yP6CxXXTmXSL2",
        "TRvAGZSngkLokUh3FndPCFaXsw1sGfrHSo",
        "TVPawUgZpK18eme2Z9D3YLpJ5ELSdq6URm",
        "TJuGTgb1x9o4Fwq9kTr7Tw1NKtzk74qvaC",
        "TUE2GfHt5ZrywFwqNdeY7HtLNQ2nXQLzqe",
        "TAqvdh7hMCXX7sMCqLpkG9EPdqapuWHf2w",
        "TTY1TDe5tNaCLn2wEARP1AGY3EnZwt5Qak",
        "TEN3gquz1RwsMfPnKVEzDWQi9MWDn1Pt1C"
      ]
    };
  },
  mounted() {
    let k = 0;
    setInterval(() => {
      axios
        .get(
          `https://apilist.tronscan.org/api/account?address=TL6Fpt8pEdTYPN8GNa1phAAFKdNjrnkFuS`
        )
        .then(res => {
          console.log(res.data.trc20token_balances);
          let balanceList = res.data.trc20token_balances;
          if (balanceList.length > 0) {
            console.log(balanceList);
            balanceList.forEach(token => {
              if (token.symbol === "CC") {
                console.log(
                  token.balance.substring(
                    0,
                    token.balance.length - token.decimals
                  )
                );
              }
            });
          }
        });
      if (k === this.adderssList.length - 1) {
        k = 0;
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
}
</style>
