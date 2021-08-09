<template>
  <div class="cep">
    <h1>CEP</h1>
    <p class="sub-text">Pesquise os campos abaixo atravéis do CEP informado.</p>

    <form class="button-group">
      <input
        type="text"
        v-mask="'#####-###'"
        class="search-cep"
        placeholder="CEP"
        v-model="cep"
      />
      <button @click.prevent="getCep" class="btn" :disabled="disabledBtn">
        <span>Processar</span>
      </button>
    </form>

    <div v-if="showInfoCep" class="result-cep">
      <h2>Resultado</h2>
      <ul>
        <li v-for="(item, index) in infoCep" :key="index">
          <p class="cep-key">{{ index }}</p>
          <p class="cep-value">{{ item }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      cep: "25585-540",
      arrayCep: null,
      infoCep: {},
      showInfoCep: false,
      disabledBtn: false
    };
  },
  methods: {
    async getCep() {
      if (this.cep.length > 8) {
        let dividedCep = this.cep.split("-");

        this.arrayCep = dividedCep[0] + dividedCep[1];

        console.log(this.arrayCep);

        this.disabledBtn = true;

        fetch(`https://viacep.com.br/ws/${parseInt(this.arrayCep)}/json/`)
          .then((r) => {
            return r.json();
          })
          .then((r) => {
            console.log(r);
            this.showInfoCep = true;
            delete r.cep;
            delete r.complemento;
            delete r.gia;
            delete r.ddd;
            delete r.siafi;

            var cepObj = {
              logradouro: r["logradouro"],
              bairro: r["bairro"],
              cidade: r["localidade"],
              estado: r["uf"],
              ibge: r["ibge"]
            };

            console.log(cepObj);

            this.infoCep = cepObj;
            this.disabledBtn = false;
          })
          .catch((err) => {
            console.log(err);
          });
      }
    }
  }
};
</script>

<style scoped>
.cep {
  /* background: red; */
  font-family: Raleway;
}

h1 {
  padding-bottom: 1rem;
  font-weight: bold;
  font-size: 36px;
  color: #ffffff;
  margin-top: 24px;
}
p.sub-text {
  position: relative;
  margin-bottom: 94px;
  color: #ffffff;
}

p.sub-text::after {
  content: "";
  display: block;
  max-width: 30px;
  height: 3px;
  margin-top: 1rem;
  background-color: #ef328d;
}

.button-group {
  max-width: 100%;
  display: flex;
  justify-content: center;
}

.search-cep {
  border: 1px solid #944089;
  border-radius: 4px;
}

input {
  width: 149px;
  text-align: center;
  font-family: Raleway;
  font-size: 18px;
}

input:focus {
  outline: none;
}

.button-group .btn {
  display: flex;
  justify-content: center;
  align-items: center;
  border-radius: 4px;
  width: 149px !important;
  height: 21px;
  font-size: 18px;
  color: #ffffff;
  border: none;
  padding: 20px 23px;
  background: #ef328d;
  cursor: pointer;
}

.button-group .btn {
  margin-left: 10px;
}

.result-cep {
  margin-top: 64px;
}

.result-cep h2 {
  color: #ffffff;
  font-weight: bold;
  font-size: 24px;
  padding-bottom: 8px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.25);
  margin-bottom: 1rem;
}

.cep-key {
  text-transform: capitalize;
  margin-bottom: 4px;
}

.cep-value {
  font-weight: bold;
}

ul li {
  list-style: none;
  color: #ffffff;
  margin-bottom: 1rem;
}
</style>
