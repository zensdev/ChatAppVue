<template>
  <div class="chat-window">
    <div class="messages">
      <div class="message" v-for="message in messages" v-bind:key="message._id">
        <div class="username">{{ message.username }}:</div>
        <div class="message-text">{{ message.msg }}</div>
      </div>
    </div>
    <form class="input-container" v-on:submit="sendMessage">
      <input type="text" v-model="msg">
      <button v-on:click="sendMessage" v-bind:disabled="!msg">Send</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ChatRoom',
  props: ['messages'],
  data: function () {
    return {
      msg: ""
    }
  },
  methods: {
    sendMessage: function () {
      if (!this.msg) {
        alert("Please enter a message");
        return;
      }

      this.$emit('sendMessage', this.msg);
      this.msg = "";
    }
  }
}
</script>

<style lang="scss" scoped>
.chat-window {
  flex: 1;
  display: flex;
  flex-direction: column;
  background-color: #F9F9F9;
  padding: 1rem;
  border-radius: 1rem;
  box-shadow: rgba(0, 0, 0, 0.241) 0px 1px 10px;

  .messages {
    flex: 1;
    overflow: scroll;

    .message {
      display: flex;
      border-bottom: 1px solid #EFEFEF;
      transition: all 0.2s ease-in-out;
      padding: 10px;

      &:last-of-type {
        border-bottom: none;
      }

      .username {
        margin-right: 15px;
        font-weight: 600;
        font-size: 18px;
      }

      .message-text {
        flex: 1;
        font-size: 18px;
      }
    }
  }

  .input-container {
    display: flex;

    input {
      flex: 1;
      height: 45px;
      padding: 0 7px;
      font-size: 18px;
      box-sizing: border-box;
      margin-right: 20px;
      border-radius: 1rem;
      outline: none;
      border: 2px solid transparent;
      box-shadow: rgba(0, 0, 0, 0.241) 0px 1px 10px;
      transition: all 0.2s ease-in-out;

      &:focus {
        box-shadow: rgba(0, 0, 0, 0.419) 0px 1px 10px;
      }
    }

    button {
      width: 100px;
      height: 45px;
      box-sizing: border-box;
      border-radius: 1rem;
      border: none;
      outline: none;
      color: black;
      font-size: 18px;
      box-shadow: rgba(0, 0, 0, 0.241) 0px 1px 10px;
      transition: all 0.2s ease-in-out;

      &:hover {
        box-shadow: rgba(0, 0, 0, 0.419) 0px 1px 10px;
      }
    }
  }
}
</style>
