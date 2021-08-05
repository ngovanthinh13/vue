<template>
  <div>
    <div v-show="login">
      <button @click="logout">Logout</button>
    </div>
    <h2>Login</h2>
    <h1>{{user}}</h1>
    <form v-on:submit.prevent="onSubmit">
      <label for="">username: </label>
      <input name="username" :value="user.name" v-on:input="user.name = $event.target.value">
      <label for="">password: </label>
      <input name="password" :value="user.pass" v-on:input="user.pass = $event.target.value">
      <br>
      <button type="submit" value="log in">Submit</button>
    </form>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "home",
  data: () => ({
    error: "",
    msg: [],
    user: {
      name: null,
      pass: null
    },
    login: false,
  }),

  mounted() {
    this.getdata()
  },
  methods: {
    getdata() {
      console.log('ddax vao getdata')
      axios
      .get('https://60678eaf98f405001728ef55.mockapi.io/api/v1/user/')
      .then(result => {
        this.msg = result;
      });
    },
    onSubmit() {
      // console.log('da vao onsubmit')
        let usernameStatus = this.msg.data.find(u => u.name === sessionStorage.getItem('usernameCurent') && u.password === sessionStorage.getItem('passwordCurent'))
        if (usernameStatus) {
          this.login = true
          console.log('Đăng nhập thành công - xin chào: ',sessionStorage.getItem('usernameCurent'))
        } else {
          console.log('Đăng nhập thất bại')
        }
    },
    logout() {
      // console.log('da vao logout')
      sessionStorage.clear()
      this.login = false
      console.log('Đã đăng xuất thành công')
    }
  },
  beforeUpdate() {
    let _usernameLocal = this.user.name;
    let _passwordLocal = this.user.pass;
    sessionStorage.setItem('usernameCurent', _usernameLocal)
    sessionStorage.setItem('passwordCurent', _passwordLocal)
  }
};

</script>


<style scoped>
input {
  margin-right: 20px
}
button {
  margin-top: 20px
}
</style>
