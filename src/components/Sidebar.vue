<template>

  <div class="sidebar">

    <div class="search">

      <input
        type="text"
        placeholder="Search"
      />

    </div>

    <div class="chat-list">

      <div
        v-for="chat in chats"
        :key="chat.id"
        class="chat-item"
      >

        <img
          :src="chat.avatar"
          class="chat-avatar"
        />

        <div class="chat-info">

          <div class="top">

            <h4>
              {{ chat.name }}
            </h4>

            <span>
              {{ chat.time }}
            </span>

          </div>

          <p>
            {{ chat.lastMessage }}
          </p>

        </div>

      </div>

    </div>

  </div>

</template>

<script>
import '../assets/styles/sidebar.css'

export default {

  data() {
    return {

      chats: [

        {
          id: 1,
          name: 'Seruy',
          lastMessage: 'Hello',
          time: '10:24',
          avatar: '/images/user1.jpg'
        },

        {
          id: 2,
          name: 'Akashi',
          lastMessage: 'Send file',
          time: '09:11',
          avatar: '/images/user2.jpg'
        },

        {
          id: 3,
          name: 'deleted',
          lastMessage: 'Audio message',
          time: 'Yesterday',
          avatar: '/images/user3.jpg'
        }

      ]

    }
  }

}
</script>