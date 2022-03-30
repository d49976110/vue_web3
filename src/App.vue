<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    123
    <button @click="metamask">click</button>
  </div>
</template>

<script>
import { ethers } from "ethers";
import HelloWorld from './components/HelloWorld.vue'

const provider = new ethers.providers.Web3Provider(window.ethereum)
console.log("provider",provider);

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  methods:{
    async metamask(){
      // await window.ethereum.request({ method: 'eth_requestAccounts' });
      window.ethereum.enable()
      console.log(123);
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
