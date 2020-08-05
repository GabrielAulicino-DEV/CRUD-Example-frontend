<template>
  <div class="form">
    <div class="container">
      <label for="uname">
        <b>Email</b>
      </label>
      <input v-model="email" type="text" placeholder="Digite seu Email" name="uname" required />

      <label for="psw">
        <b>Senha</b>
      </label>
      <input v-model="password" type="password" placeholder="Digite sua Senha" name="psw" required />

      <button @click="login()" type="submit">Login</button>
      <button @click="redirect()" type="submit">Criar Conta</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "Login",
  data() {
    return {
      name: "",
      email: "",
      password: "",
    };
  },
  props: {
    method: { type: Function },
  },
  methods: {
    redirect() {
      this.method("signUp");
    },
    login() {
      axios
        .post("http://localhost:3333/user/login", {
          email: this.email,
          password: this.password,
        })
        .then((response) => {
          const token = response.data.data.token;
          localStorage.setItem("bearer ", token);
          this.method("logged", token);
        })
        .catch((error) => {
            this.$notify({
            group: "foo",
            type: "error",
            title: "Preencha os Campos Corretamente!",
          });
          console.log(error);
        });
    },
  },
  created() {},
};
</script>


<style scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

input[type="text"],
input[type="password"] {
  width: 100%;
  padding: 12px 20px;
  margin: 8px 0;
  display: inline-block;
  border: 1px solid #ccc;
  box-sizing: border-box;
}

button {
  background-color: purple;
  color: white;
  padding: 14px 20px;
  margin: 8px 0;
  border: none;
  cursor: pointer;
  width: 100%;
}

.container {
  padding: 30px;
}
</style>
