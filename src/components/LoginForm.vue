<template>
  <div>
    <h2>ログイン</h2>
    <form @submit.prevent="login">
      <input type="email" required placeholder="メールアドレス" v-model="email">
      <input type="password" required placeholder="パスワード" v-model="password">
      <button>ログインする</button>
      <div class="error">{{ error }}</div>
    </form>
  </div>
</template>

<script>
import axios from 'axios'
import setItem from '../auth/setItem'

export default {
  emits: ['redirectToChatRoom'],
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
    methods: {
    async login() {
      try {
        this.error = null

        const res = await axios.post('http://localhost:3000/auth/sign_in', {
          email: this.email,
          password: this.password,
          }
        )
        if (!res) {
          throw new Error('メールアドレスかパスワードが違います')
        }
        if (!this.error) {
          // localStorageに保存する
          setItem(res.headers, res.data.data.name)
          this.$emit('redirectToChatRoom')
        }
        console.log({ res })
        return res
      } catch (error) {
        console.log({ error })
        this.error = 'メールアドレスかパスワードが違います'
      }
    }
  }
}
</script>
