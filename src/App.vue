<script setup>
import { io } from 'socket.io-client';
import { onBeforeMount, ref } from 'vue';

const socket = io('http://localhost:5555');

const messages = ref([]);

onBeforeMount(() => {
  socket.emit('findAllMessages', (data) => {
    messages.value = data;
  });
});
</script>

<template>
  <div class="chat">
    <div class="chat-container">
      <div class="messages-container">
        <div v-for="message in messages">
          [{{ message.name }}]: {{ message.text }}
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import './assets/main.css';
</style>
