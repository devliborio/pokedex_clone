<template>
  <div id="app"></div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
    data() {
    return {
      pokemons: [] // Variável que vai receber
    };
  },
  created: function () { // Método que é chamado toda vez que o componente é carregado na aplicação.
    
    // Acessando o Objeto Data e o Array onde contem todos os Pokemon's da primeira geração.
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((res) => {this.pokemons = res.data.results;}).catch((err) => console.log(err));
  },
};
</script>

<style>
</style>
