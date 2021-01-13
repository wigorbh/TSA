<template>
  <div>
    <h1>Lista</h1>
    <p>Lista de Clientes</p>
    <hr />
    <p>Nome do Cliente</p>
    <input type="text" />

    <table>
      <tr>
        <th>Nome</th>
        <th>Email</th>
        <th>Cpf</th>
        <th>Criado em</th>
      </tr>
      <p v-if="false" />
      <tr v-for="user in usersRegistered" :key="user.user">
        <td>{{ usersRegistered.user }}</td>
        <td>{{ usersRegistered.email }}</td>
        <td>{{ usersRegistered.cpf }}</td>
        <td>{{ usersRegistered.date}}</td>
      </tr>
    </table>
    <Footer />
  </div>
</template>

<script>
import Footer from '../components/Footer';

export default {
  name: "List",
  data() {
    return {
      usersRegistered: [{
        user: "",
        email: "",
        cpf: "",
        date: "",
      }],
    };
  },
  components: {
    Footer
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
</style>