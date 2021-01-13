<template>
  <div>
    <div class="title">
      <h1 class="title-align">Lista</h1>
    </div>
    <div class="container">
      <p class="title-blue">Lista de Clientes</p>
      <hr />
      <label class="label" for="name">Nome do Cliente</label >
      <input id="name" class="input-style position-full" type="text" />
      <table class="table">
        <tr>
          <th>Nome</th>
          <th>Email</th>
          <th>Cpf</th>
          <th>Criado em</th>
        </tr>
        <tr v-for="user in usersRegistered" :key="user.user">
          <td>{{ usersRegistered.user }}</td>
          <td>{{ usersRegistered.email }}</td>
          <td>{{ usersRegistered.cpf }}</td>
          <td>{{ usersRegistered.date }}</td>
        </tr>
      </table>
    </div>
    <Footer />
  </div>
</template>

<script>
import Footer from "../components/Footer";

export default {
  name: "List",
  data() {
    return {
      usersRegistered: [
        {
          user: "",
          email: "",
          cpf: "",
          date: "",
        },
      ],
    };
  },
  components: {
    Footer,
  },
  created() {
    this.usersRegistered.user = this.$route.params.name;
    this.usersRegistered.email = this.$route.params.email;
    this.usersRegistered.cpf = this.$route.params.cpf;
    this.usersRegistered.date = this.$route.params.date;
  },
};
</script>

<style lang="scss" scoped>
.table {
  border: solid black 1px;
  margin-top: 1rem;
  text-align: center;
  width: 100%;
}
</style>