<template>
  <div class="register">
    <header>
      <button>Lista</button>
      <button>Cadastro</button>
    </header>
    <h1 class="a">Cadastro</h1>
    <div class="container">
      <label class="label">Nome</label>
      <input class="input" type="text" />
      <label class="label">Email</label>
      <input class="input" type="text" />
      <label class="label">CPF</label>
      <input class="input" type="number" placeholder="111.111.111-01" />

      <div class="j">
        <div>
          <label class="">Endereço</label>
          <input type="text" class="" placeholder="Rua, Número e Bairro" />
        </div>
        <div>
        <label class="">Estado</label>
        <select class="">
          <option disabled selected hidden>Selecione o Estado</option>
          <option v-for="state in BrazilState" :key="state">{{ state }}</option>
        </select>
        </div>
      </div>
      <label class="label">CEP</label>
      <input type="number" class="" placeholder="22.222-000" />
      <label>Cidade</label>
      <select class="">
        <option disabled selected hidden>Selecione a Cidade</option>
        <option v-for="capital in stateCapitals" :key="capital">
          {{ capital }}
        </option>
      </select>
 
        <p>Forma de Pagamento</p>
        <hr>
        <input type="radio" >
        <label>Cartão de Crédito</label>
        <input type="radio" >
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
    <Footer />
  </div>
</template>

<script>
import Footer from './Footer.vue'

export default {
  name: "Register",
  data() {
    return {
      BrazilState: ["Minas Gerais", "São Paulo", "Rio de Janeiro", "Paraná"],
      stateCapitals: ["São Paulo", "Belo Horizonte", "Rio de Janeiro"],
    };
  },
  methods: {},
  components: {
    Footer
  }
};
</script>

<style scoped>
.container {
  margin: 2em auto;
  width: 65%;
}

.input {
  height: 2rem;
  width: 90%;

}

.label {
  /* background: green; */
  display: flex;
}

.a {
  background: #dde0e2;
  height: 4.5rem;
  margin-left: 15%;
}

.j {
  display: flex;
}
</style>