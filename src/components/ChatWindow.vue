<template>
  <div class="chat-window">
    <div class="messages">
      <div
        v-for="(msg, index) in messages"
        :key="index"
        :class="['message', msg.sender]"
      >
        {{ msg.text }}
      </div>
    </div>
    <form class="input-area" @submit.prevent="handleSend">
      <input v-model="text" placeholder="Type a message..." />
      <button type="submit">Send</button>
    </form>
  </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps({
  messages: {
    type: Array,
    required: true
  }
})

const emit = defineEmits(['send'])
const text = ref('')

function handleSend() {
  if (!text.value.trim()) return
  emit('send', text.value)
  text.value = ''
}
</script>

<style scoped>
.chat-window {
  flex: 1;
  display: flex;
  flex-direction: column;
  height: 100vh;
  background: #fafafa;
}
.messages {
  flex: 1;
  padding: 1rem;
  overflow-y: auto;
}
.message {
  margin-bottom: 0.5rem;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  max-width: 70%;
}
.message.user {
  align-self: flex-end;
  background: #4e54c8;
  color: #fff;
  text-align: right;
}
.message.bot {
  background: #e0e0e0;
  align-self: flex-start;
}
.input-area {
  display: flex;
  padding: 1rem;
  border-top: 1px solid #eee;
  background: #fff;
}
.input-area input {
  flex: 1;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}
.input-area button {
  margin-left: 0.5rem;
  padding: 0.5rem 1rem;
  background: #4e54c8;
  border: none;
  color: #fff;
  border-radius: 4px;
}
</style>
