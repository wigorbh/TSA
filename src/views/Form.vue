<template>
  <div class="register">
    <h1 class="">Cadastro</h1>
    <div class="container">
      <label class="label">Nome</label>
      <input v-model="name" class="input" type="text" />
      <p v-if="name.length < 10 && name.length > 2">
        Nome deve ter no mínimo 10 caracteres
      </p>

      <label class="label">Email</label>
      <input v-model="email" class="input" type="text" />
      <p v-if="email.length < 10 && email.length > 2">Digite um email válido</p>

      <label class="label">CPF</label>
      <input class="input" type="number" placeholder="111.111.111-01" />
      <p v-if="cpf.length < 10 && cpf.length > 2">CPF com 11 digitos</p>

      <div class="flex">
        <div class="input-row">
          <label>Endereço</label>
          <input class="input" type="text" placeholder="Rua, Número e Bairro" />
        </div>
        <div class="input-row">
          <label class="">Estado</label>
          <select class="input-select" v-model="UF">
            <option disabled selected hidden>Selecione o Estado</option>
            <option v-for="state in BrazilState" :key="state.id">
              {{ state.sigla }}
            </option>
          </select>
        </div>
      </div>
      <div class="flex">
        <div class="input-row">
          <label class="">CEP</label>
          <input type="number" class="input" placeholder="22.222-000" />
        </div>
        <div class="input-row">
          <label>Cidade</label>
          <select class="input-select">
            <option disabled selected hidden>Selecione a Cidade</option>
            <option v-for="district in districts" :key="district.id">
              {{ district.nome }}
            </option>
          </select>
        </div>
      </div>
      <p class="title-blue">Forma de Pagamento</p>
      <hr />
      <div class="flex">
        <input type="radio" />
        <label>Cartão de Crédito</label>
        <input type="radio" />
        <label>Boleto Bancário</label>
      </div>
      <br />
      <div class="flex">
        <div class="input-row">
          <label>Nome no Cartão</label>
          <input type="text" class="input" placeholder="Nome impresso no cartão" />
        </div>
        <div class="input-row">
          <label>Data de Expiração</label>
          <div class="flex">
          <select class="input-select">
            <option disabled selected hidden>Mês</option>
            <option v-for="mounth in mounths" :key="mounth">
              {{ mounth }}
            </option>
          </select>
          <select class="input-select">
            <option disabled selected hidden>Ano</option>
            <option v-for="year in years" :key="year">{{ year }}</option>
          </select>
          </div>
        </div>
      </div>
      <br />
      <div class="flex">
        <div class="input-row">
          <label>Número do Cartão</label>
          <input type="text" class="input" placeholder="5555 5555 5555 5555" />
        </div>
        <div class="input-row">
          <label>Código de Segurança</label>
          <input type="text" class="input" placeholder="XXX" />
        </div>
      </div>
      <hr />
      <div>
        <p>Seu cartão será debitado em R$ 49,00</p>
        <button class="button-submit">REALIZAR MATRÍCULA</button>
        <p>Informações seguras e criptografadas</p>
      </div>
    </div>
    <Footer />
  </div>
</template>

<script>
import axios from "axios";
import Footer from "../components/Footer";

export default {
  name: "Register",
  data() {
    return {
      BrazilState: [],
      UF: "",
      districts: [],
      mounths: [
        "Janeiro",
        "Fevereiro",
        "Março",
        "Abril",
        "Maio",
        "Junho",
        "Julho",
        "Agosto",
        "Setembro",
        "Outubro",
        "Novembro",
        "Dezembro",
      ],
      years: [
        "2021",
        "2022",
        "2023",
        "2024",
        "2025",
        "2026",
        "2027",
        "2028",
        "2029",
        "2030",
      ],
      name: "",
      email: "",
      cpf: 0,
      street: "",
    };
  },
  methods: {
    submitForm() {
      const name = this.name;
      const email = this.email;
      const cpf = this.cpf;
      const street = this.street;

      const regex = /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/;

      if (!name) return false;
      if (regex.test(email)) return true;
      if (!cpf) return false;

      if (name && email && cpf && street) {
        return; // enviar para o back-end;
      }
    },
  },
  components: {
    Footer,
  },
  created() {
    axios
      .get("https://servicodados.ibge.gov.br/api/v1/localidades/estados")
      .then(({ data }) => (this.BrazilState = data))
      .catch((err) => console.error(err));
  },
  updated() {
    axios
      .get(
        `https://servicodados.ibge.gov.br/api/v1/localidades/estados/${this.UF}/distritos`
      )
      .then(({ data }) => (this.districts = data))
      .catch((err) => console.error(err));
  },
};
</script>

<style lang="scss" scoped>
.container {
  margin: 2em auto;
  width: 50%;
  .label {
    display: flex;
  }
}

.flex {
  display: flex;
  align-items: center;
}

.input-row {
  display: flex;
  flex-direction: column;
  width: 90%;
  .input-select {
    // margin-left: 12px;
    height: 39.5px;
    width: 95%;
  }
}

.input {
  height: 2rem;
  width: 97%;
}

.title-blue {
  color: #1188ee;
}

.button-submit {
  background: #1188ee;
  border-radius: 5px 5px;
  border-style: none;
  color: #fff;
  text-align: center;
  height: 50px;
  width: 45%;
}

.button-submit:active {
  box-shadow: rgb(23, 156, 14) 2px 2px;
}

// .a {
//   background: #dde0e2;
//   height: 4.5rem;
//   margin-left: 15%;
// }
</style>