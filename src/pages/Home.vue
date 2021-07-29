<template>
  <div class="home">
    <!-- <Card v-for="item in dados" :key="item.id" :dadoscadastrados="dados" /> -->
    <div class="card" v-for="item in dados" :key="item.id">
      <div class="nome">
        <p>{{ item.nome }}</p>
      </div>
      <div class="nome">
        <p>{{ item.email }}</p>
      </div>
      <div class="nome">
        <p>{{ item.sobrenome }}</p>
      </div>
      <div class="nome">
        <a @click="deletarDados($event, item.id)" href="#">
          <img src="@/assets/excluir.svg" alt="img-excluir " />
        </a>
      </div>
    </div>
    <div class="buttons">
      <button class="cadastrarnovo" @click="viajar">
        Cadastrar Novo
      </button>
      <button class="cadastrarnovo" @click="viajarlogin">
        Finalizar login
      </button>
    </div>
  </div>
</template>
<script>
// import Card from "@/components/Card";
import axios from "axios";
export default {
  data() {
    return {
      dados: [],
    };
  },
  mounted() {
    this.carregarDados();
  },
  components: {
    // Card,
  },
  methods: {
    async carregarDados() {
      const { data } = await axios.get("http://localhost:3000/peoples");
      this.dados = data;
      console.log(dados);
    },
    viajar() {
      this.$router.push("/cadastrados");
    },
    viajarlogin() {
      this.$router.push("/");
    },
    async deletarDados(e, id) {
      e.preventDefault();
      const { data } = await axios.delete(
        `http://localhost:3000/peoples/${id}`
      );
      this.carragarDados();
    },
  },
};
</script>

<style scoped>
.home {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
.card {
  width: 80%;
  height: 60px;
  background: #fff;
  border-radius: 4px;
  box-shadow: 3px 3px 12px red;
  margin: 10px;
  display: flex;
  justify-content: space-around;
}
.nome {
  padding: 10px;
}
.cadastrarnovo {
  width: 140px;
  height: 60px;
  border-radius: 5px;
  border-style: none;
  margin: 10px;
  background: rgba(107, 3, 3, 0.63);
  color: #fff;
  font-size: 15px;
}
.cadastrarnovo:hover {
  /* background: red; */
  background: rgb(175, 28, 28);
  font-size: 17px;
  /* width: 250px; */
  /* font-size: 25px; */
}
.buttons {
  width: 80%;
  background: #303030;
  display: flex;
  justify-content: space-around;
}
</style>
