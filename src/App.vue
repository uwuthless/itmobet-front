<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <LoginPass v-bind:balance="balance"/>
    <FindEvent v-on:new-events="refreshEvents" />
    <EventHolder v-bind:events="this.events" v-on:balance-changed="updateBalance"/>
  </div>

</template>

<script>

import axios from 'axios';
import Vue from 'vue';
import VueCookies from 'vue-cookies';
Vue.use(VueCookies)
// set default config
VueCookies.config('7d')

import LoginPass from "./components/LoginPass";
import FindEvent from "./components/FindEvent";
import EventHolder from "./components/EventHolder";



export default {
  name: 'app',
  components: {
    LoginPass,
    FindEvent,
    EventHolder
  },
  methods: {
    refreshEvents(eventsArray) {

      this.events = eventsArray;
      window.console.log(this.events)
    },
    async updateBalance() {
      const _id = VueCookies.get('_id')
      if (_id) {
        const userData = (await axios.get(`http://localhost:3000/user/balance?_id=${_id}`)).data
        this.balance = userData.balance
      }
    }
  },
  data(){
    return{
      events: [],
      balance:0
    }
  },
  async created() {
      await this.updateBalance()
    }
  }

</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
