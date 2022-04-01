<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HelloWorld msg="Welcome to Your Vue.js App" />
    <button @click="connect">click</button>

    <div>
      <label for="">Balance</label>
      <h5>{{ balance }}</h5>
    </div>
  </div>
</template>

<script>
import {ethers} from 'ethers';
import HelloWorld from './components/HelloWorld.vue';
import {abi} from './contracts/abi.js';

export default {
  name: 'App',
  components: {
    HelloWorld,
  },
  async created() {
    await window.ethereum.request({method: 'eth_requestAccounts'});
  },
  data() {
    return {
      balance: 0,
    };
  },
  methods: {
    async connect() {
      await window.ethereum.request({method: 'eth_requestAccounts'});

      const provider = await new ethers.providers.Web3Provider(window.ethereum);
      const signer = await provider.getSigner();
      let erc20 = await new ethers.Contract(
        '0xd7e64966E98126802FA38A56d2d0B4F7E91934f3',
        abi,
        signer
      );
      const wallet_balance = await erc20.balanceOf(signer.getAddress());
      this.balance = wallet_balance;
      // console.log('balance', balance.toNumber());
    },
  },
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
</style>
