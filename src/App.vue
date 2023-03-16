<template>
  <div id="app">

    <div class="column is-half is-offset-one-quarter">
      <h1 class="title is-2">Pokedex com Vue.js</h1>
      <input class="input is-rounded" type="text" placeholder="Buscar Pokemon pelo nome" v-model="search">
      <div v-for='(poke,index) in resultSearch' :key="poke.url"> 
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
      pokemons: [], // Variável que vai receber os dados da Poke API
      search: ''
    };
  },
  created: function () { // Método que é chamado toda vez que o componente é carregado na aplicação.
    
    // Acessando o Objeto Data e o Array onde contem todos os Pokemon's da primeira geração.
    axios.get("https://pokeapi.co/api/v2/pokemon?limit=151&offset=0").then((res) => {this.pokemons = res.data.results;}).catch((err) => console.log(err));
  },

  components: {
    Pokemon
  },

  computed: {
    resultSearch: function(){
      if(this.search == '' || this.search == ' '){
         return this.pokemons;
      } else {
        return this.pokemons.filter(pokemon => pokemon.name == this.search)
      }
    }
  }
};
</script>

<style>
  #app{
    text-align: center;
    margin-top: 60px;
    margin-bottom: 60px;
  }

  #searchBtn{
    margin-top: 2%;
    margin-bottom: 8%;
  }
</style>
