<template>
  <img alt="Vue logo" src="./assets/logo.png" />
  <button @click="sendMessage()">Send mess</button>
</template>

<script>
import { io } from 'socket.io-client';
export default {
  name: 'App',
  setup() {
    var socket = io('http://localhost:3000');

    socket.on('connect', () => {
      console.log(`connected with id: ${socket.id}`);
    });

    socket.on('receive-mess', (message) => {
      console.log(`mensagem recebida ${message}`);
    });

    const sendMessage = () => {
      socket.emit('custom-event', 10222, 'saazasdasdasdsa');
    };
    return { socket, sendMessage };
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
