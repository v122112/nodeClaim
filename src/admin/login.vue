<template>
  <form class="form">
    <label for="username">Имя пользователя</label>
    <input type="text" name="username" id="username" />
    <label for="password">Пароль</label>
    <input type="password" name="password" id="password" />
    <div
      class="button"
      @click="login"
    >
      Вход
    </div>
    <div
      class="error red"
      v-if="error !== ''"
    >
      {{ error }}
    </div>
  </form>
</template>

<script>
import sha256 from 'crypto-js/sha256'
import Base64 from 'crypto-js/enc-base64'

export default {
  name: 'Login',
  props: ['error'],
  methods: {
    login () {
      this.$emit('login', {
        username: document.getElementById('username').value,
        password: Base64.stringify(sha256(document.getElementById('password').value)),
      })
    },
  },
}
</script>

<style lang="sass" scoped>
.form
  position: absolute
  z-index: 11000
  display: flex
  flex-flow: column nowrap
  align-items: center
  width: 100%
  margin: calc(50vh - 150px) auto auto auto
  padding: 20px

input, label, div
  margin: 5px
  min-width: 300px
  text-align: left

.button
  background: #13aa13
  padding: 10px
  text-align: center
</style>
