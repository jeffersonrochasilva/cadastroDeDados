<template>
  <div class="modal">
    <div class="container">
      <input v-model="nome" type="text" placeholder="digite seu nome" />
      <input
        v-model="sobrenome"
        type="text"
        placeholder="digite seu sobrenome"
      />
      <input v-model="email" type="e-mail" placeholder="Digite seu E-mail" />
      <input v-model="password" type="text" placeholder="Digite sua idade" />
      <input
        v-model="confirmarsenha"
        type="text"
        placeholder="confirme sua senha"
      />
      <div class="buttons">
        <button @click="save">Cadastrar</button>
        <button @click="voltar">Voltar</button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      nome: "",
      sobrenome: "",
      email: "",
      confirmarsenha: "",
      password: "",
    };
  },
  props: {
    modal: Boolean,
  },
  methods: {
    async save() {
      if (this.senha === this.confirmarSenha) {
        const data = await axios.post("http://localhost:3000/peoples", {
          nome: this.nome,
          sobrenome: this.sobrenome,
          email: this.email,
          password: this.password,
        });
        alert("Usuario cadastrado");
        this.$router.push("/");
      } else {
        alert("Senha não são iguais");
      }
    },
    voltar() {
      this.$router.push("/");
    },
  },
};
</script>

<style scoped>
.modal {
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  box-shadow: 8px 8px 8px 8px #fcc419;
  position: fixed;
  left: 0;
  top: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
.container {
  width: 600px;
  height: 400px;
  background: #303030;
  border-radius: 4px;
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
}

input {
  width: 80%;
  height: 40px;
  text-align: center;
  border-radius: 5px;
  border-style: none;
}
.buttons {
  width: 80%;
  display: flex;
  justify-content: space-around;
}
button {
  width: 120px;
  height: 40px;
  border-radius: 4px;
  border-style: none;
  background: rgba(107, 3, 3, 0.63);
  color: #fff;
}
button:hover {
  width: 160px;
  background: red;
  color: #fff;
}
</style>
