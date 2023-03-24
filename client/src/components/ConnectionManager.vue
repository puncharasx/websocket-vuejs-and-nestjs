<template>
  <button @click="connect()">Connect</button>
  <button @click="emit()">Emit (event)</button>
  <button @click="disconnect()">Disconnect</button>
</template>

<script>
import { io } from 'socket.io-client'
export default {
  name: "ConnectionManager",

  methods: {
    connect() {
      const socket = io("https://aef5-182-232-187-229.ap.ngrok.io")
      socket.on('connect',() => {
          console.log('Connected');
        }
      )
      socket.on('payment', (data) => {
        alert('Payment success')
        console.log('payment', data)
      })
    },
    disconnect() {
      // socket.disconnect();
    },
    emit() {
      const socket = io("http://localhost:3001")
      socket.on('connect',() => {
          console.log('Connected');
        }
      )
      socket.on('events', function(data) {
        console.log('event', data);
      });

      socket.emit('events', { test: 'testasdasdasd' });
    }
  }
}
</script>