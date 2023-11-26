<template>
  <div class="message-list">
    <div v-for="(message, index) in messages" :key="index" :class="[message.sender, 'message']">
      {{ message.text }}
    </div>
  </div>
</template>

<script>
export default {
  props: {
    messages: Array,
  },
};
</script>

<style lang="stylus" >
.message-list
  display flex
  flex-direction column
  max-height 300px
  overflow-y auto

.message
  margin-bottom 10px
  padding 8px
  border-radius 4px

.user
  align-self flex-end
  background-color #007bff
  color #fff
  margin-right 10px

.bot
  align-self flex-start
  background-color #28a745
  color #fff
  margin-left  10px
</style>

