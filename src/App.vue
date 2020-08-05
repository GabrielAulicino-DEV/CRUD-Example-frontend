<template>
  <div id="app">
    <div v-if="option ==='signUp'">
    <SignUp :method="parentMethode"></SignUp>
    </div>
    <div v-else-if="option ==='login'">
    <Login :method="parentMethode"></Login>
    </div>
    <div style="text-align: -webkit-center;" v-else-if="option ==='logged'">
    <Profile :method="parentMethode" :token="token"></Profile>
    </div>
    <div v-else-if="option ==='editprofile'">
    <EditProfile :method="parentMethode" :token="token"></EditProfile>
    </div>
    <notifications group="foo" />
  </div>
</template>

<script>
import SignUp from './components/SignUp.vue'
import Login from './components/Login.vue'
import Profile from './components/Profile.vue'
import EditProfile from './components/EditProfile.vue'

export default {
  name: 'App',
  data(){
    return{
      option: 'login',
      token: "",
    }
  },
  components: {
    Login,
    Profile,
    SignUp,
    EditProfile
  },
    methods: {
    parentMethode(valuefromChild, token){
      this.option = valuefromChild
      this.token = token
      // console.log(token)
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
