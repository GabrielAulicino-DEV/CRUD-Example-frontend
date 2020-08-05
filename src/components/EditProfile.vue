<template>
  <div class="form">
    <div class="container">
      <label for="uname">
        <b>Nome Editar</b>
      </label>
      <input v-model="token.name" type="text" name="uname" />
      <label for="cpf">
        <b>CPF</b>
      </label>
      <input v-model="token.cpf" type="text" placeholder="Digite seu CPF" name="cpf" required />

      <label for="uname">
        <b>Email</b>
      </label>
      <input v-model="token.email" type="text" placeholder="Digite seu Email" name="uname" required />

      <button @click="editUser()" type="submit">Editar Usuário</button>
      <button @click="cancelEditUser()" type="submit">Cancelar</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "EditProfile",
  props: {
    method: { type: Function },
    token: { type: Object },
  },
  data() {
    return {
      //   user: {}
    };
  },
  methods: {
    cancelEditUser(){
        this.method("logged")
    },
    editUser() {
      const userData = localStorage.getItem("bearer ");
      // console.log("DATA", userData)
      const instance = axios.create({
        headers: {
          Authorization: `bearer ${userData}`,
        },
      });
      instance
        .post("http://localhost:3333/user/update", {
          name: this.token.name,
          email: this.token.email,
          cpf: this.token.cpf,
        })
        .then(() => {
            this.method("logged")
          this.$notify({
            group: "foo",
            type: "success",
            title: "Informações Alteradas com Sucesso!",
          });
        })
        .catch((err) => {
          console.log(err);
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
