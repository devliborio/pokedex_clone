<template>
  <div>
    <h1>{{ num }} {{ upper(name) }}</h1>
    <small>{{ url }}</small>

    <div class="card">
    <div class="card-image">
        <figure class="image is-4by3">
        <img src="https://bulma.io/images/placeholders/1280x960.png" alt="Placeholder image">
        </figure>
    </div>
    <div class="card-content">
        <div class="media">
            <div class="media-content">

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
        })
    },

    data(){
        return{
            pokemon: {}
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

<style>
</style>