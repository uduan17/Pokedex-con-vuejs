<template>
  <nav class="navbar navbar-expand-lg bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="#"><img src="../../public/poe.png"></a>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
    </div>
  </div>
</nav>
 <br>

 <h3><img src="../../public/pokebola.png" alt="" style="width:85px"> -----------> <img src="../../public/pikachu.png" alt="" style="width:85px"></h3>

  <div class="container">
    <div class="d-flex justify-content-center flex-wrap ">

      <!----------------Card------------------------>
        <div class="card mx-3 mt-4 shadow " style="width: 18rem" v-for="pokemon, index in pokemons" :key="index">
            <!-- Button trigger modal -->
            <a @click="showPokemonModal(pokemon.url)">

          <img :src="`https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/official-artwork/${index + 1}.png`" />
          <div class="card-body">
          <h5 class="card-title">{{ pokemon.name }}</h5>
        </div>
        </a>
      </div>

    </div>
</div>

<!-- Modal -->
<div v-if="load"> <ModalPokemon :pokemonUrl="pokemonUrl" /> </div>

<br><br>
</template>
      
<script>
import axios from "axios";
import ModalPokemon from "./ModalPokemon.vue";
import * as bootstrap from 'bootstrap'

export default {
  name: "PokemonList",
  components : {
    ModalPokemon
  },

  data(){
    return {
      pokemons : null,
      pokemonUrl: '',
      load : false,
      modal: null
    }
  },

     mounted(){
     this.getPokemons()
    },

// llamando a todos los pokemones
    methods: {
      async getPokemons(){
        const response = await axios.get("https://pokeapi.co/api/v2/pokemon/?limit=32");
        this.pokemons = response.data.results;
      },

// funcion que llama al modal
      showPokemonModal(url) {
        this.load = true 
        this.mostrarModal()
        this.pokemonUrl = url
      },
      
// mostrar modal
    mostrarModal() {
      this.load = true
      setTimeout(() => {
                this.modal = new bootstrap.Modal(
                    document.getElementById('exampleModal'), 
                    { keyboard: false }
                )
                this.modal.show()

                const modal = document.getElementById('exampleModal')
                modal.addEventListener('hidden.bs.modal', () => {
                    this.load = false
                })
            }, 200)
    },
    ocultarModal() {
      this.modal.hide()
    }
  }
};
</script>
  
<style scoped>
a{
    cursor: pointer;
}

img{
  width: 203px;
}
.card:hover{
  transform: scale(1.07);
}
.card{
  transition: transform 0.5s;
  background: radial-gradient(circle, rgba(112,57,82,0.17130602240896353) 32%, rgba(77,125,181,0.14889705882352944) 77%);
  font-family: 'Nunito', sans-serif;
  }
</style>