<template>
  <div id="pokemon">
    <div class="card">

        <div class="card-image">
            <figure>
                <img :src="pokemon.front">
            </figure>
        </div>

        <div class="card-content">

            <div class="media">

                <div class="media-content">
                    <p class="title is-4">{{ num }} - {{ upper(name) }}</p>
                    <p class="subtitle is-5">{{ pokemon.type }}</p>
                </div>

            </div>

            <div class="content">

            </div>
      </div>

    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {

    created: function(){
        axios.get(this.url).then((res) => {
            this.pokemon.type = res.data.types[0].type.name; 
            this.pokemon.front = res.data.sprites.front_default; 
            this.pokemon.back = res.data.sprites.back_default;
            // Uma observação importante é que as variáveis (type, front e back se forem cridas somente pela requisição do axios ela não será reativa no HTML então se você quiser reatividade você terá que definir ela dentro do método data(){}.
        })
    },

    data(){
        return{
            pokemon: {
                type: '',
                front: '',
                back: ''
            }
        }
    },

    props: {
        num: Number,
        name: String,
        url: String
    },

    methods: { // Agora os filtros podem ser usado como métodos normais
        upper: function (value) {
            let newName = value[0].toUpperCase() + value.slice(1); 
            return newName;
        }    
    }
}
</script>

<style scoped>
    #pokemon {
        margin-top: 2%;
    }
</style>