<template>

  <div class="chat-input">

    <input
      v-model="message"
      placeholder="Write a message..."
      @keyup.enter="sendText"
    />

    <label class="icon-btn">

      <Image :size="20" />

      <input
        type="file"
        accept="image/*"
        hidden
        @change="uploadImage"
      />

    </label>

    <label class="icon-btn">

      <Paperclip :size="20" />

      <input
        type="file"
        hidden
        @change="uploadFile"
      />

    </label>

    <button
      class="icon-btn"
      @click="toggleRecording"
    >

      <Mic
        v-if="!isRecording"
        :size="20"
      />

      <Square
        v-else
        :size="20"
      />

    </button>

    <button
      class="send-btn"
      @click="sendText"
    >

      <Send :size="20" />

    </button>

  </div>

</template>

<script>
import '../assets/styles/input.css'

import {
  Send,
  Mic,
  Image,
  Paperclip,
  Square
} from 'lucide-vue-next'

export default {

  components: {
    Send,
    Mic,
    Image,
    Paperclip,
    Square
  },

  data() {

    return {

      message: '',

      mediaRecorder: null,
      audioChunks: [],

      isRecording: false

    }

  },

  methods: {

    // SEND TEXT
    sendText() {

      if (!this.message.trim()) return

      this.$emit(
        'send-message',
        this.message
      )

      this.message = ''

    },

    uploadImage(event) {

      const file =
        event.target.files[0]

      if (!file) return

      const imageUrl =
        URL.createObjectURL(file)

      this.$emit(
        'send-image',
        imageUrl
      )

    },

    uploadFile(event) {

      const file =
        event.target.files[0]

      if (!file) return

      const fileUrl =
        URL.createObjectURL(file)

      this.$emit(
        'send-file',
        {
          name: file.name,
          url: fileUrl
        }
      )

    },

    async toggleRecording() {

      if (!this.isRecording) {

        try {

          const stream =
            await navigator
            .mediaDevices
            .getUserMedia({
              audio: true
            })

          this.mediaRecorder =
            new MediaRecorder(stream)

          this.audioChunks = []

          this.mediaRecorder.start()

          this.isRecording = true

          this.mediaRecorder.ondataavailable =
            (event) => {

            this.audioChunks.push(
              event.data
            )

          }

          this.mediaRecorder.onstop =
            () => {

            const audioBlob =
              new Blob(
                this.audioChunks,
                {
                  type: 'audio/webm'
                }
              )

            const audioUrl =
              URL.createObjectURL(
                audioBlob
              )

            this.$emit(
              'send-audio',
              audioUrl
            )

          }

        } catch (error) {

          alert(
            'Microphone access denied'
          )

        }

      } else {

        this.mediaRecorder.stop()

        this.isRecording = false

      }

    }

  }

}
</script>