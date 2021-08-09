<template>
  <div class="home">
    <h1>Texto</h1>
    <p class="sub-text">
      Filtre o texto abaixo capturando somente as palavras trissílabas.
    </p>

    <div class="text-container">
      <div v-html="text"></div>
    </div>

    <button @click.prevent="getWordsResult" class="btn">
      <span>Processar</span>
    </button>

    <div class="result-total" v-if="showResultWord">
      <h2>Resultado</h2>
      <p>Total: {{ trisyllableWords.length }}</p>
    </div>

    <div class="result-word" v-if="showResultWord">
      <div
        v-for="(array, index) in arrayOfArrays"
        :key="index"
        class="word-value"
      >
        <div v-for="(item, index) in array" :key="index">
          <p>{{ index }}. {{ item }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { syllable } from "stress-pt";

export default {
  name: "Texto",
  data() {
    return {
      trisyllableWords: [],
      columnTotal: null,
      wordsLength: null,
      count: 1,
      masterArray: [],
      arrayOfArrays: [],
      showResultWord: false,
      text:
        'O programa espacial da China deu um enorme salto ao colocar com sucesso a sonda Zhurong em Marte, assinalando a primeira aterragem da China noutro planeta. As equipas estão agora a preparar-se para tirar a sonda da sua plataforma de aterragem para iniciar uma missão que visa procurar evidências de água e indícios de vida passada. <br /> <br /> Esta aterragem torna a China no segundo país da história a colocar uma  sonda na superfície de Marte. Depois de meses a orbitar o planeta vermelho, a nave Tianwen-1 lançou a sonda Zhurong para aterrar em Utopia Planitia, uma vasta planície que pode ter estado coberta por um      antigo oceano marciano. A sonda de 240 quilos sobreviveu a uma perigosa descida até à superfície, incluindo a entrada atmosférica, desacelerar de velocidades supersónicas com um paraquedas e, por fim,   usar foguetões para pousar com segurança no solo. <br /> <br /> Batizada em homenagem ao antigo deus chinês do fogo, a sonda Zhurong é semelhante em tamanho às sondas Spirit e Opportunity da NASA, que aterraram no planeta vermelho em 2004 e enviaram imagens e dados emocionantes sobre as condições da superfície do planeta. A sonda chinesa pode fazer descobertas adicionais importantes sobre a água e a habitabilidade do planeta no passado, abrindo caminho para futuras missões humanas a Marte. <br /> <br /> “Aterrar com segurança em Marte é um enorme desafio, sobretudo para a primeira tentativa de aterragem suave da China”, diz Long Xiao,cientista planetário da Universidade de Geociências da China. “Mas é um passo necessário para a exploração de Marte e do espaço profundo. <br /> <br />"Descer com sucesso até à superfície de Marte é um desafio extraordinário. Até agora, só a NASA é que tinha aterrado e operado naves com segurança na superfície marciana; em 1971, a sonda soviética Mars 3 transmitiu metade de uma fotografia, antes de ficar em silêncio depois de uma missão que durou apenas 100 segundos. Ao aterrar e explorar Marte, a China ganha vantagem sobre uma série de pares na exploração espacial. <br /> <br /> A sonda Zhurong conseguiu sobreviver aos chamados “sete minutos de terror”, o tempo desde a entrada na atmosfera até à aterragem na superfície. A Administração Espacial Nacional da China (CNSA) limitou-se observar a aterragem autónoma a quase 320 milhões de quilómetros de distância – tão longe que demora 18 minutos a receber um sinal de Marte – e esperar que corresse tudo conforme planeado. <br /> <br /> A Zhurong estava acoplada ao seu companheiro orbital, envolta numa cobertura que foi projetada para proteger o veículo no seu trajeto através da atmosfera marciana. Depois de libertada e de passar por uma entrada atmosférica abrasadora, foi ativado um enorme paraquedas para abrandar ainda mais a descida da sonda.<br /> <br /> Depois, a plataforma de aterragem que segura a sonda acionou os foguetões do motor para fazer a aproximação final à superfície. Um localizador de alcance a laser e um scanner 3D forneceram os dados sobre a altitude e terreno enquanto as câmaras a bordo escolheram autonomamente um local para aterrar.'
    };
  },

  methods: {
    countText() {
      let textQuebrado = this.text.split(" ");
      textQuebrado.forEach((item, index) => {
        console.log("index: ", index);
        let wordSplited = syllable(item);

        let silabas = wordSplited.split("|");
        console.log("silabas: ", silabas);

        if (silabas.length === 3) {
          let normalWord = silabas.join("");

          this.trisyllableWords.push(normalWord);
          this.wordsLength = this.trisyllableWords.length;
        }
      });

      console.log(textQuebrado);
    },

    getWordsResult() {
      var arr = this.trisyllableWords;

      for (let key in arr) {
        arr["index"] = key;
        console.log("key kkk", key);
      }

      var tamanho = 5;
      var novoArray = [];
      var i = 0;

      while (i < arr.length) {
        novoArray.push(arr.slice(i, i + tamanho));

        i += tamanho;
      }
      this.showResultWord = true;

      // console.log("kkkkkk: ", novoArray);

      return (this.arrayOfArrays = novoArray);
    }
  },
  created() {
    this.countText();
  }
};
</script>

<style scoped>
* {
  list-style-type: none;
}
.home {
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

.text-container {
  max-width: 100%;
  height: 300px;
  padding: 24px;
  background: rgba(255, 255, 255, 0.9);
  border: 1px solid #944089;
  box-sizing: border-box;
  backdrop-filter: blur(4px);
  border-radius: 4px;

  margin: 10px;
}

.text-container div {
  max-width: 100%;
  max-height: 100%;
  overflow-y: scroll;
}

::-webkit-scrollbar {
  width: 14px;
}

::-webkit-scrollbar-track {
  background-color: #e8d9e7;
  border: 2px solid #f1ebf2;
  opacity: 0.1;
  border-radius: 100px;
}

::-webkit-scrollbar-thumb {
  border: 4px solid rgba(0, 0, 0, 0);
  background-clip: padding-box;
  border-radius: 9999px;
  background-color: #6d1d63;
}

.result-word {
  display: flex;
  flex-wrap: wrap;
  justify-content: flex-start;
  margin-top: 64px;
}

.btn {
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
  margin: 32px auto;
}
.result-total {
  max-width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}

.result-total p {
  color: #ffffff;
  font-weight: bold;
}

h2 {
  color: #ffffff;
  font-weight: bold;
  font-size: 24px;
  padding-bottom: 8px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.25);
}

.word-value {
  color: #ffffff;
  font-weight: bold;
}

.word-value {
  margin-right: 73px;
  margin-top: 50px;
}
</style>
