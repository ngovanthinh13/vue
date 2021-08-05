<template>
  <div>
    <h2>Login</h2>
    <h1>{{user}}</h1>
    <form >
      <label for="">username: </label>
      <input name="username" :value="user.name" v-on:input="user.name = $event.target.value">
      <label for="">password: </label>
      <input name="password" :value="user.pass" v-on:input="user.pass = $event.target.value">
      <br>
      <button type="submit" value="log in">Submit</button>
    </form>
    <!-- <button @click="getdata">Get data</button> -->
  </div>
</template>

<script>
// import { defineComponent } from '@vue/composition-api'
// import { mapState, mapActions } from 'vuex'
import axios from 'axios';
// const API_URL = "https://60678eaf98f405001728ef55.mockapi.io/api/v1/";

export default {
  name: "home",
  data: () => ({
    error: "",
    msg: [],
    user: {
      name: null,
      pass: null
    }
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
