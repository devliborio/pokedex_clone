<template>
  <div id="app">

    <div class="column is-half is-offset-one-quarter">
      <div v-for='(poke,index) in pokemons' :key="index"> 
      <Pokemon :name="poke.name" :url="poke.url" :num="index + 1" />
    </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'
export default {
  name: 'App',
    data() {
    return {
      pokemons: [] // Variável que vai receber
    };
  },
  created: function () { // Método que é chamado toda vez que o componente é carregado na aplicação.
    
    // Acessando o Objeto Data e o Array onde contem todos os Pokemon's da primeira geração.
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((res) => {this.pokemons = res.data.results;}).catch((err) => console.log(err));
  },

  components: {
    Pokemon
  }
};
</script>

<style>
</style>
