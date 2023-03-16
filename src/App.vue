<template>
  <div id="app"></div>
</template>

<script>
import axios from "axios";

export default {
  name: "App",
  created: function () {
    // Método que é chamado toda vez que o componente é carregado na aplicação.
    axios
      .get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0")
      .then((res) => {
        console.log(res.data.results); // Acessando o Objeto Data e o Array onde contem todos os Pokemon's da primeira geração.
      })
      .catch((err) => console.log(err));
  },
};
</script>

<style>
</style>
