<template>
<div>
    <form @submit.prevent="onSubmit(username, password)">
        <div class="form-group">
            <label for="username">Username</label>
            <input type="text" v-model="username" name="username" class="form-control" :class="{ 'is-invalid': submitted && !username }" />
            <div v-show="submitted && !username" class="invalid-feedback">Username is required</div>
        </div>
        <div class="form-group">
            <label htmlFor="password">Password</label>
            <input type="password" v-model="password" name="password" class="form-control" :class="{ 'is-invalid': submitted && !password }" />
            <div v-show="submitted && !password" class="invalid-feedback">Password is required</div>
        </div>
        <div class="form-group">
            <button class="btn">Login</button>
            <router-link to="/register" class="btn btn-link">Register</router-link>
        </div>
    </form>
</div>
</template>
<script>
export default {
  data () {
    return {
      username: '',
      passowrd: '',
      msg: '',
      submitted: false
    }
  },
  methods: {
    onSubmit (username, passowrd) {
      this.submitted = true
      if (username == null || passowrd == null) {
        alert('ID 또는 Password를 입력해주세요.')
        return
      }
      alert('id : ' + username + ' ' + 'pwd : ' + passowrd)
      // LOGIN 액션 실행
      // this.$store.dispatch('LOGIN', {email, password})
      //  .then(() => this.redirect())
      //  .catch(({message}) => this.msg = message)
    },
    redirect () {
      const { search } = window.location
      const tokens = search.replace(/^\?/, '').split('&')
      const { returnPath } = tokens.reduce((qs, tkn) => {
        const pair = tkn.split('=')
        qs[pair[0]] = decodeURIComponent(pair[1])
        return qs
      }, {})

      // 리다이렉트 처리
      this.$router.push(returnPath)
    }
  }
}
</script>
