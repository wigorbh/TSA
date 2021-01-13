<template>
  <div class="register">
    <div class="title">
      <h1 class="title-align">Cadastro</h1>
    </div>
    <form action="" v-on:submit.prevent="checkForm" class="container">
      <label class="label" for="name">Nome</label>
      <input id="name" v-model="name" class="input-style position-full" type="text" />
      <p class="warning" v-if="name.length < 10 && name.length > 2">
        Digite o nome completo
      </p>

      <label class="label">Email</label>
      <input v-model="email" class="input-style position-full" type="text" />
      <p class="warning" v-if="email.length < 10 && email.length > 2">
        email no formato exemplo@email.com
      </p>

      <label class="label">CPF</label>
      <input
        v-model="cpf"
        class="input-style position-full"
        type="number"
        placeholder="111.111.111-01"
      />
      <p class="warning" v-if="cpf.length < 10 && cpf.length > 2">
        CPF com 11 digitos
      </p>

      <div class="flex">
        <div class="input-row">
          <label class="label">Endereço</label>
          <input
            v-model="street"
            class="input-style position-half-start"
            type="text"
            placeholder="Rua, Número e Bairro"
          />
          <p class="warning" v-if="street.length < 10 && street.length > 2">
            Digite endereço completo
          </p>
        </div>
        <div class="input-row">
          <label for="state" class="label" >Estado</label>
          <select id="state" class="input-select position-half-end" v-model="UF">
            <option disabled selected hidden>Selecione o Estado</option>
            <option v-for="state in BrazilState" :key="state.id">
              {{ state.sigla }}
            </option>
          </select>
        </div>
      </div>
      <div class="flex">
        <div class="input-row">
          <label class="label" for="cep">CEP</label>
          <input
            id="cep"
            v-model="cep"
            type="number"
            class="input-style position-half-start"
            placeholder="22.222-000"
          />
          <p class="warning" v-if="cep.length < 10 && cep.length > 2">
            mínimo 8 digitos
          </p>
        </div>
        <div class="input-row">
          <label class="label" for="city">Cidade</label>
          <select id="city" v-model="city" class="input-select position-half-end">
            <option disabled selected hidden>Selecione a Cidade</option>
            <option v-for="district in districts" :key="district.id">
              {{ district.nome }}
            </option>
          </select>
        </div>
      </div>
      <br>
      <p class="title-blue">Forma de Pagamento</p>
      <hr />
      <div class="flex">
        <input type="radio" name="selected" />
        <label class="label">Cartão de Crédito</label>
        <input type="radio" name="selected" />
        <label class="label">Boleto Bancário</label>
      </div>
      <br />
      <div class="flex">
        <div class="input-row">
          <label class="label">Nome no Cartão</label>
          <input
            type="text"
            class="input-style position-half-start"
            placeholder="Nome impresso no cartão"
          />
        </div>
        <div class="input-row ">
          <label class="label">Data de Expiração</label>
          <div class="flex position-half-end">
            <select class="input-select">
              <option disabled selected hidden>Mês</option>
              <option v-for="mounth in mounths" :key="mounth">
                {{ mounth }}
              </option>
            </select>
            <select class="input-select" style="margin-left: 15px">
              <option disabled selected hidden>Ano</option>
              <option v-for="year in years" :key="year">{{ year }}</option>
            </select>
          </div>
        </div>
      </div>
      <br />
      <div class="flex">
        <div class="input-row">
          <label class="label">Número do Cartão</label>
          <input
            type="text"
            class="input-style position-half-start"
            placeholder="5555 5555 5555 5555"
          />
        </div>
        <div class="input-row">
          <label class="label" >Código de Segurança</label>
          <input
            type="text"
            class="input-style position-half-end"
            placeholder="XXX"
          />
        </div>
      </div>
      <br>
      <hr />
      <div>
        <p>Seu cartão será debitado em R$ 49,00</p>
        <button class="button-submit">REALIZAR MATRÍCULA</button>
        <p>Informações seguras e criptografadas</p>
      </div>
      <ul>
        <li class="warning" v-for="error in errors" :key="error">{{ error }}</li>
      </ul>
    </form>
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
      cpf: "",
      street: "",
      UF: "",
      cep: "",
      city: "",
      date: "",
      errors: [],
    };
  },
  methods: {
    checkForm() {
      this.errors = [];
      if (!this.name) {
        this.errors.push("O nome deve ser preenchido");
      }
      if (!this.email) {
        this.errors.push("Digite um email válido");
      }
      if (!this.cpf) {
        this.errors.push("Digite o Cpf");
      } else {
        this.$router.push({
          name: "list",
          params: {
            name: this.name,
            email: this.email,
            cpf: this.cpf,
            date: new Date()
              .toLocaleString()
              .split(/\D/)
              .slice(0, 3)
              .map((num) => num.padStart(2, "0"))
              .join("/"),
          },
        });
        alert("Cadastrado com sucesso");
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

<style lang="scss" >
.button-submit {
  background: #1188ee;
  border-radius: 5px 5px;
  border-style: none;
  color: #fff;
  text-align: center;
  height: 50px;
  width: 45%;
}

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
  width: 100%;
}

.input-select {
  height: 2.5rem;
  width: 100%;
  background: #eff4f9;
  border: none;
  border-radius: 4px;
  box-shadow: 0px 2px 4px rgba(187, 204, 221, 0.4);

}

.input-style {
  background: #eff4f9;
  border: none;
  border-radius: 4px;
  box-shadow: 0px 2px 4px rgba(187, 204, 221, 0.4);
}

.label {
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
  font-size: 1.2rem;
}

.position-full {
  height: 2.5rem;
  width: 100%;
}

.position-half-start {
  height: 2.5rem;
  width: 95%;
  align-self: flex-start;
}

.position-half-end {
  height: 2.5rem;
  width: 95%;
  align-self: flex-end;
}

.title-blue {
  color: #1188ee;
  font-size: 1.2rem;
  margin-bottom: 0.5rem;
}

.title {
  background: #eff4f9;
  height: 6rem;
}

.title-align {
  font-family: "Nunito", sans-serif;
  font-size: 4rem;
  margin-left: -5em;
  color: #445566;
  text-align: center;
}

.register {
  margin-bottom: 10rem;
  width: 100%;
}

.warning {
  color: #ff0000;
  font-size: 15px;
  list-style: none;
}

@media screen and (max-width: 600px) {
  .container {
    margin: 1em auto;
    width: 90%;
  }
  .title-align {
    margin-left: 0.1em;
  }
}
</style>