<template>

  <div
    v-if="!isAuthenticated"
    class="auth-page"
  >

    <div class="auth-box">

      <h1>Telegram</h1>

      <input
        v-model="login"
        placeholder="Login"
      />

      <input
        v-model="password"
        type="password"
        placeholder="Password"
      />

      <button @click="authorize">
        Log In
      </button>

    </div>

  </div>

  <div
    v-else
    class="app"
  >

    <Sidebar />

    <div class="chat-container">

      <ChatHeader />

      <MessageList
        :messages="messages"
      />

      <ChatInput
        @send-message="sendMessage"
        @send-image="sendImage"
        @send-file="sendFile"
        @send-audio="sendAudio"
      />

    </div>

  </div>

</template>

<script>
import Sidebar from './components/Sidebar.vue'
import ChatHeader from './components/ChatHeader.vue'
import MessageList from './components/MessageList.vue'
import ChatInput from './components/ChatInput.vue'

import './assets/styles/app.css'

export default {

  components: {
    Sidebar,
    ChatHeader,
    MessageList,
    ChatInput
  },

  data() {

    return {

      login: '',
      password: '',

      isAuthenticated: false,

      messages: [

        {
          text: 'Hello Wrld!',
          time: '14:22'
        }

      ]

    }

  },

  methods: {

    authorize() {

      if (
        this.login === 'admin'
        &&
        this.password === '1234'
      ) {

        this.isAuthenticated = true

      } else {

        alert('Wrong login or password')

      }

    },

    getCurrentTime() {

      const now = new Date()

      return now.toLocaleTimeString([], {
        hour: '2-digit',
        minute: '2-digit'
      })

    },

    sendMessage(text) {

      this.messages.push({

        text,

        time: this.getCurrentTime()

      })

    },

    sendImage(image) {

      this.messages.push({

        image,

        time: this.getCurrentTime()

      })

    },

    sendFile(file) {

      this.messages.push({

        file,

        time: this.getCurrentTime()

      })

    },

    sendAudio(audio) {

      this.messages.push({

        audio,

        time: this.getCurrentTime()

      })

    }

  }

}
</script>