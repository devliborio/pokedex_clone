<template>
  <div id="pokemon">
    <div class="card">

        <div class="media-content">
            <p class="title is-4">{{ upper(name) }}</p>
        </div>

        <div class="card-image">
            <figure>
                <img :src="currentImg">
            </figure>
        </div>

        <div class="card-content">

            <div class="media">

                <div class="media-content">
                    <p class="title is-5">Tipo</p>
                    <p class="subtitle is-5"> - {{ pokemon.type_one }}</p>
                    <p class="subtitle is-5">{{ pokemon.type_two }}</p>
                </div>

                <div class="media-content">
                    <p class="title is-5"> Habilidade </p>
                    <p class="subtitle is-5"> - {{ pokemon.habilidade }}</p>
                </div>

            </div>

            <div class="content">
                <button class="button is-normal is-success is-light is-fullwidth" @click="changeSprite">Girar</button>
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
            this.pokemon.type_one = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default; 
            this.pokemon.back = res.data.sprites.back_default;
            this.pokemon.habilidade = res.data.abilities[0].ability.name;
            this.currentImg = this.pokemon.front;
            console.log(res)
            // Uma observação importante é que as variáveis (type, front e back se forem cridas somente pela requisição do axios ela não será reativa no HTML então se você quiser reatividade você terá que definir ela dentro do método data(){}.
        })
    },

    data(){
      return{
        isFront: true,
        currentImg: '',

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

        changeSprite: function(){
             if(this.isFront){
                    this.isFront = false;
                    this.currentImg = this.pokemon.back;
            } else {
                     this.isFront = true;
                     this.currentImg = this.pokemon.front;
            }
        },

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