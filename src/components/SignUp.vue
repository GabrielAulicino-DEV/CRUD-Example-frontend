<template>
  <div class="form">
    <div class="container">
      <label for="uname">
        <b>Nome</b>
      </label>
      <input v-model="name" type="text" placeholder="Digite seu Nome" name="uname" required />
      <label for="cpf">
        <b>CPF</b>
      </label>
      <input v-model="cpf" type="text" placeholder="Digite seu CPF" name="cpf" required />

      <label for="uname">
        <b>Email</b>
      </label>
      <input v-model="email" type="text" placeholder="Digite seu Email" name="uname" required />

      <label for="psw">
        <b>Senha</b>
      </label>
      <input v-model="password" type="password" placeholder="Digite sua Senha" name="psw" required />

      <button @click="createUser()" type="submit">Criar Conta</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SignUp",
  data() {
    return {
      name: "",
      email: "",
      cpf: "",
      password: "",
    };
  },
  props: {
    method: { type: Function },
  },
  methods: {
    async createUser() {
      try {
        let res = await axios.post("http://localhost:3333/user/create", {
          name: this.name,
          cpf: this.cpf,
          email: this.email,
          password: this.password,
        });
        this.method("login");
        this.$notify({
          group: "foo",
          type: "success",
          title: "Usuário Criado com Sucesso!",
        });
        return res.data;
      } catch (err) {
        this.$notify({
          group: "foo",
          type: "error",
          title: "Preencha os campos corretamente",
        });
      }
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
