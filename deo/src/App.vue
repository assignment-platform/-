<template>
  <div id="app">
   <div v-if="!logined">
     <input type="text" v-model="form.username">
     <br>
     <input type="password" v-model="form.password">
     <br>
     <button @click="login">登录</button>
   </div>
   <div v-if="logined">
     <button @click="about">查看个人资料</button>
     <h2>Welcome,{{myName}}</h2>
   </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import Axios from "axios";

export default {
  name: 'app',
  data() {
    return {
      form: {
         username:"",
         password:"",
         name:""
        }
    };
  },
  methods: {
    login(){
      Axios.post("http://localhost:8081/login",this.form)
      .then(response =>(this.logined=true))
      .catch(error =>console.error(error));
      },
      about(){
        Axios.get("http://localhost:8081/about")
        .then(response =>(this.myName =response.data.name))
        .catch(error =>console.error(error));
      }
      }
}
</script>

<style>

</style>
