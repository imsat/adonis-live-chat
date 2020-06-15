<template>
  <div id="app">
    <h1>Chat Room</h1>
    <input
      type="text"
      v-model="inputMessage"
      @keyup.enter="sendMessage(inputMessage)"
    />
    <button @click="sendMessage(inputMessage)">Send</button>

    <ul>
      <li
        v-for="(message, index) in messages"
        :key="index"
        v-html="message"
        style="list-style: none;"
      ></li>
    </ul>
    <!-- <router-view /> -->
  </div>
</template>

<script>
import Ws from "@adonisjs/websocket-client";
const ws = Ws("ws://localhost:3333");
export default {
  name: "App",
  data() {
    return {
      chat: null,
      messages: [],
      inputMessage: ""
    };
  },
  async created() {
    this.initializeChatWs();
  },
  methods: {
    async initializeChatWs() {
      await ws.connect();

      this.chat = ws.subscribe("chat");
      let chat = this.chat;
      // chat.on("ready", () => {
      //   this.sendMessage("Hello there");
      //   // chat.emit("message", "hello");
      // });

      chat.on("message", event => {
        this.receiveMessage(event);
      });
    },
    async sendMessage(message) {
      this.chat.emit("message", message);
      this.inputMessage = "";
    },
    async receiveMessage(msg) {
      this.messages.push(msg);
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
