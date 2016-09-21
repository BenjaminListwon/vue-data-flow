<template>
  <div>
    <h1>{{ clientid }}</h1>
    <div class="client">
      <ul>
          <li v-for="message in messages">
            <label>{{ message.sender }}:</label> {{ message.text }}
          </li>
      </ul>
      <div class="msgbox">
        <input v-model="msg" placeholder="Enter a message, then hit [enter]" @keyup.enter="trySendMessage">
      </div>
    </div>
  </div>
</template>

<script>
import { mapState, mapActions } from 'vuex'

export default {
  data() {
    return {
      msg: ''
    }
  },
  props: ['clientid'],
  computed: {
    ...mapState({
      messages: state => state.messages
    })
  },
  methods: {
    trySendMessage() { 
      this.newMessage({
        text: this.msg, 
        sender: this.clientid
      })
      this.resetMessage()
    },
    resetMessage() {
      this.msg = ''
    },
    ...mapActions(['newMessage'])
  }
}
</script>
