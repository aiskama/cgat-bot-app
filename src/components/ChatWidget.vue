<template>
  <div class="chat-widget">
    <MessageList :messages="messages" />
    <div class="options" v-if="options.length > 0">
      <p>{{ botGreeting }}</p>
      <button v-for="(option, index) in options" :key="index" @click="selectOption(option)">
        {{ option }}
      </button>
    </div>
    <div class="user-input">
      <input v-model="userInput" @keyup.enter="sendMessage" placeholder="Введите сообщение..." />
    </div>
  </div>
</template>

<script>
import MessageList from './MessageList.vue';

export default {
  components: {
    MessageList,
  },
  data() {
    return {
      messages: [],
      userInput: '',
      options: ['Заказать пиццу', 'Установить будильник', 'Вывести погоду'],
      botGreeting: 'Привет! Что я могу для Вас сделать?',
    };
  },
  mounted() {
    this.botReply(this.botGreeting, this.options);
  },
  methods: {
    sendMessage() {
      if (this.userInput.trim() === '') return;

      this.messages.push({ text: this.userInput, sender: 'user' });
      this.processUserInput(this.userInput);

      this.userInput = '';
    },
    processUserInput(userInput) {
      if (this.options.includes(userInput)) {
        this.botReply(`Хорошо, я ${userInput.toLowerCase()}. Что еще могу сделать?`, this.options);
      } else {
        this.botReply('Извините, я не понял ваш запрос. Что еще могу сделать?', this.options);
      }
    },
    botReply(text, options) {
      this.messages.push({ text, sender: 'bot', options });
    },
    selectOption(option) {
      this.messages.push({ text: option, sender: 'user' });
      this.processUserInput(option);
    },
  },
};
</script>

<style lang="stylus" >
.chat-widget
  max-width 400px
  margin 0 auto
  border 1px solid #ccc
  border-radius 8px
  overflow hidden

.user-input
  background-color #f4f4f4
  padding 10px

input
  width calc(100% - 20px)
  padding 8px
  margin 5px 0
  border 1px solid #ccc
  border-radius 4px

.options
  margin-top 10px

.options p
  margin-bottom 10px

.options button
  margin 5px
  padding 5px 10px
  background-color #007bff
  color #fff
  border none
  border-radius 4px
  cursor pointer

.options button:hover
  background-color #0056b3
</style>
