<template>
  <div class="register">
    <h1 class="">Cadastro</h1>
    <div class="container">
      <label class="label">Nome</label>
      <input v-model="name" class="input" type="text" />
      <p v-if="name.length < 10 && name.length > 2">Nome deve ter no mínimo 10 caracteres</p>
      <label class="label">Email</label>
      <input  v-model="email" class="input" type="text" />
      <p v-if="email.length < 10 && email.length > 2">Digite um email válido</p>
      <label class="label">CPF</label>
      <input class="input" type="number" placeholder="111.111.111-01" />

      <div style="display:flex">
        <div class="hj">
          <label >Endereço</label>
          <input type="text" class="" placeholder="Rua, Número e Bairro" />
        </div>
        <label class="">Estado</label>
        <div class="hj">
        <select  v-model="UF" class="">
          <option disabled selected hidden>Selecione o Estado</option>
          <option v-for="state in BrazilState" :key="state.id">{{ state.sigla }}</option>
        </select>
        </div>
      </div>

      <label class="">CEP</label>
      <input type="number" class="" placeholder="22.222-000" />
      <label>Cidade</label>
      <select class="">
        <option disabled selected hidden>Selecione a Cidade</option>
        <option v-for="district in districts" :key="district.id">
          {{ district.nome }}
        </option>
      </select>
 
        <p>Forma de Pagamento</p>
        <hr>
        <input type="radio" >
        <label>Cartão de Crédito</label>
        <input  type="radio" >
        <label>Boleto Bancário</label>

        <label>Nome no Cartão</label>
        <input type="text" class="" placeholder="Nome impresso no cartão">

        <label>Data de Expiração</label>
        <select>
          <option disabled selected hidden>Mês</option>
          <option>Janeiro</option>
        </select>
          <select>
          <option disabled selected hidden>Ano</option>
          <option>2022</option>
        </select>

        <label>Número do Cartão</label>
        <input type="text" class="" placeholder="5555 5555 5555 5555">
        <label>Código de Segurança</label>
        <input type="text" class="" placeholder="XXX">
  
      <hr>
      <div>
        <p>Seu cartão será debitado em R$ 49,00</p>
        <button>REALIZAR MATRÍCULA</button>
        <p>Informações seguras e criptografadas</p>
      </div>

    </div>
    <!-- <Footer /> -->
  </div>
</template>

<script>
// import Footer from './Footer.vue'
import axios from 'axios';



export default {
  name: "Register",
  data() {
    return {
      BrazilState: [],
      UF: "",
      districts: [],
      name: "",
      email: "",
      cpf: 0,
      street: "",
    };
  },
  methods: {
    // submit(){
    //   const name = this.name;
    // chama aqui a request para city
    // }
  },
  components: {
    // Footer
  },
  // computed: {
  //   validName() {
  //     if (this.name.length < 10 && this.name.length > 1) {
  //       return  "Nome pequeno"
  //     }
  //     return ""
  //   }
  // }
  created(){
    axios.get("https://servicodados.ibge.gov.br/api/v1/localidades/estados")
    .then(({data}) => this.BrazilState = data)
    .catch(err => console.error(err));
    
  },
  updated(){
    axios.get(`https://servicodados.ibge.gov.br/api/v1/localidades/estados/${this.UF}/distritos`)
    .then(({data}) => this.districts = data)
    .catch(err => console.error(err));
  }
};


</script>

<style lang="scss" scoped>
.container {
  margin: 2em auto;
  width: 65%;
  .label {
    display: flex;
  }
}

.hj {
  display:flex;
  flex-direction:column
}
.input {
  height: 2rem;
  width: 90%;
}

.a {
  background: #dde0e2;
  height: 4.5rem;
  margin-left: 15%;
}


</style>