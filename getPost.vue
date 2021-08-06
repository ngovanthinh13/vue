<template>
  <div>
    <div v-show="$store.state.StateLogin">
      <button @click="logout">Logout</button>
    </div>
    <ul>
      <li v-for="(item) in posts.data" :key="item.id">
        <a>{{item.title}}</a>
        <p>{{item.content}}</p>
        <strong>{{item.author.name}}</strong>
        </li>
    </ul>
    <h2>{{$store.state.StateLogin}}</h2>
    <!-- <p>{{posts.data}}</p> -->
  </div>
</template>

<script>
import axios from 'axios';
import {mapState } from 'vuex';


export default {
  name: "home",
  computed: {
    ...mapState([
      // 'user'
    ])
  },
  data: () => ({
    posts: [],
    user: {
      name: null,
      pass: null
    },
  }),
// EvLUhXRcGzbgCPe pass || ngovanthinh13
  mounted() {
    this.getdata();
  },
  methods: {
    getdata() {
      console.log('Đã vào hàm getData')
      axios
      .get('https://60678eaf98f405001728ef55.mockapi.io/api/v1/post')
      .then(result => {
        this.posts = result;
      });
    },
    logout() {
      // console.log('da vao logout')
      sessionStorage.clear()
      this.$store.state.StateLogin = false;
      this.login = false
      this.user.name = null
      this.user.pass = null
      console.log('Đã đăng xuất thành công')
    }
  },
  beforeUpdate() {
    // console.log(this.posts)
    // let _usernameLocal = this.user.name;
    // let _passwordLocal = this.user.pass;
    // sessionStorage.setItem('usernameCurent', _usernameLocal)
    // sessionStorage.setItem('passwordCurent', _passwordLocal)
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
