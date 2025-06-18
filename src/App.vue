<template>
  <div class="app">
    <ChatSidebar
      :conversations="conversations"
      :selectedId="selectedId"
      @select="selectConversation"
    />
    <ChatWindow
      v-if="activeConversation"
      :messages="activeConversation.messages"
      @send="sendMessage"
    />
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import ChatSidebar from './components/ChatSidebar.vue'
import ChatWindow from './components/ChatWindow.vue'

const conversations = ref([
  {
    id: 1,
    title: 'Conversation 1',
    messages: [
      { text: 'Hello', sender: 'user' },
      { text: 'Hi there!', sender: 'bot' }
    ]
  },
  { id: 2, title: 'Conversation 2', messages: [] }
])

const selectedId = ref(conversations.value[0].id)

const activeConversation = computed(() =>
  conversations.value.find(c => c.id === selectedId.value)
)

function selectConversation(id) {
  selectedId.value = id
}

function sendMessage(text) {
  const conv = activeConversation.value
  conv.messages.push({ text, sender: 'user' })
  // Placeholder bot response
  conv.messages.push({ text: '...', sender: 'bot' })
}
</script>

<style>
.app {
  display: flex;
  height: 100vh;
  background: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>
