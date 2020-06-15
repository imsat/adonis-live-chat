<template>
  <div id="app">
    <h1>Chat Room</h1>
    <input type="text" v-model="inputMessage" />
    <button @click="sendMessage">Send</button>
    <!-- <router-view /> -->
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      ws: null,
      inputMessage: ""
    };
  },
  async created() {},
  methods: {
    async sendMessage() {
      alert(this.inputMessage);
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
