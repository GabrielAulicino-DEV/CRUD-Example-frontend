<template>
  <div class="card">
    <img src="@/assets/logo.png" alt="Avatar" style="width:50%" />
    <div class="container">
      <h4>
        <b>{{user.name}}</b>
      </h4>
      <p>{{user.cpf}}</p>
      <p>{{user.email}}</p>
    </div>
    <button @click="editProfile(user)" type="submit">Editar</button>
    <br>
    <button @click="logout()" type="submit">Sair</button>
  </div>
</template>
<script>
import axios from "axios";
export default {
  props: {
    method: { type: Function },
    token: { type: String },
  },
  data() {
    return {
      user: {},
    };
  },
  methods: {
    editProfile(token){
      this.method("editprofile", token)
      // console.log("Editando", token)
    },
    getUser() {
      const userData = localStorage.getItem("bearer ");
      // console.log("DATA", userData)
      const instance = axios.create({
        headers: {
          Authorization: `bearer ${userData}`,
        },
      });
      instance
        .get("http://localhost:3333/user")
        .then((res) => {
          this.user = res.data.user;
        })
        .catch((err) => {
          console.log(err);
        });
    },
    logout(){
      this.method("login")
    }
  },
  created() {
    this.getUser();
  },
};
</script>

<style scoped>
.card {
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: 0.3s;
  width: 40%;
}

.container {
  padding: 2px 16px;
}
button {
  background-color: purple;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 50%;
}
</style>
