<template>
  <div>
    <h1>PODE IR DORMIR {{usersRegistered}} </h1>
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
      <tr v-for="obj in object" :key="obj.date">
        <td>{{ name }}</td>
        <td>{{ email }}</td>
        <td>{{ cpf }}</td>
        <td>{{ date }}</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  name: "List",
  data(){
    return {
      usersRegistered: []
    }
  },
  // props: {
  //   age: { type: String },
  // },
  created(){
    this.usersRegistered = this.$route.params.data
  }
};
</script>

<style lang="scss" scoped>
</style>