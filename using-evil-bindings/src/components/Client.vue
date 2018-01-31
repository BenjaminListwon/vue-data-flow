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
const events = {
  sendMessage: 'sendMessage'
}

export default {
  data() {
    return {
      msg: ''
    }
  },
  props: ['clientid', 'messages'],
  methods: {
    trySendMessage() { 
      this.$emit(events.sendMessage, {
        text: this.msg, 
        sender: this.clientid
      })
      this.resetMessage()
    },
    resetMessage() {
      this.msg = ''
    }
  }
}
</script>
