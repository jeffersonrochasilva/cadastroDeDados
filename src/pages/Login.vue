<template>
  <div id="app">
    <div class="container">
      <img src="@/assets/logo-signa.svg" alt="logo signa" />
      <input
        class="campo"
        type="e-mail"
        placeholder="E-mail "
        v-model="email"
      />
      <input
        class="campo"
        type="password"
        placeholder="Senha"
        v-model="password"
      />
      <div class="recuperar">
        <a href="">Esqueci minha senha</a>
      </div>
      <button @click="submit" class="buttonEnter">ENTRAR</button>
      <button class="buttonCadastro" @click="mudar">quero me cadastrar</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      email: "",
      password: "",
    };
  },
  components: {},
  methods: {
    mudar() {
      this.$router.push("/cadastrados");
    },
    async submit(e) {
      e.preventDefault();
      const { data } = await axios.get("http://localhost:3000/peoples", {
        params: {
          email: this.email,
          password: this.password,
        },
      });
      if (data.length > 0) {
        // alert("logando..");
        this.$router.push("/home");
      } else {
        alert("usuario ou senha incorretos");
      }
    },
  },
};
</script>

<style lang="scss" scoped>
#app {
  height: 100%;
  background: #303030;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.container {
  height: 50%;
  width: 50%;
  display: flex;
  align-items: center;
  flex-direction: column;
  justify-content: space-around;
}

.campo {
  width: 328px;
  height: 56px;
  border-radius: 4px;
  border-style: none;
}

.recuperar {
  width: 328px;
}

.buttonEnter {
  height: 48px;
  width: 331px;
  border-radius: 4px;
  border-style: none;
  // background: #6202ee;
  background: rgba(107, 3, 3, 0.63);
  font-size: 16px;
  color: #fff;
}

.buttonEnter:hover {
  background: rgb(175, 28, 28);
}

.buttonCadastro {
  height: 48px;
  width: 331px;
  background: #303030;
  border: 1px solid #fff;
  border-radius: 4px;
  font-size: 16px;
  color: #fff;
}
a {
  text-decoration: none;
  color: #fff;
}
</style>
