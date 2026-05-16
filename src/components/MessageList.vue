<template>

  <div class="messages">

    <div
      v-for="(message, index) in messages"
      :key="index"
      class="message"
    >

      <p v-if="message.text">
        {{ message.text }}
      </p>

      <img
        v-if="message.image"
        :src="message.image"
        class="image"
      />

      <audio
        v-if="message.audio"
        controls
        :src="message.audio"
      ></audio>

      <a
        v-if="message.file"
        :href="message.file.url"
        target="_blank"
        class="file"
      >
        📁 {{ message.file.name }}
      </a>

      <div class="message-time">

        {{ message.time }}

      </div>

    </div>

  </div>

</template>

<script>
import '../assets/styles/messages.css'

export default {

  props: {
    messages: Array
  }

}
</script>