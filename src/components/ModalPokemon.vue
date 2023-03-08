<template>
  <!-- Modal -->
  <div
    class="modal fade"
    id="exampleModal"
    tabindex="-1"
    aria-labelledby="exampleModalLabel"
    aria-hidden="true"
  >
    <div class="modal-dialog">
      <div class="modal-content">
        <div class="modal-header border border-0">
          <h1 class="modal-title fs-5" id="exampleModalLabel"></h1>
          <button
            type="button"
            class="btn-close bg-white"
            data-bs-dismiss="modal"
            aria-label="Close"
          ></button>
        </div>

        <!---------------------- CARD-POKEMON---------------->
        <div class="card border border-0 mb-3" style="max-width: 540px">
          <div class="row g-0">
            <h2 class="card-title mb-1">{{ pokemon.name }}</h2>

            <div class="col-md-6">
              <img :src="pokemon.image" alt="" />
            </div>

            <div class="col-md-3">
              <br />
              <strong>Abilities</strong>
              <p v-for="(item, index) in pokemon.abilities" :key="index">
                {{ item.ability.name }}
              </p>
              <strong>Types</strong>
              <p v-for="(item, index) in pokemon.types" :key="index">
                {{ item.type.name }}
              </p>
            </div>

            <div class="col-md-3">
              <br />
              <strong>experience</strong>
              <p class="mt-1">{{ pokemon.base_experience }}</p>
              <strong>Weight</strong>
              <p class="mt-1">{{ pokemon.weight }}</p>
              <strong>Order</strong>
              <p class="mt-1">{{ pokemon.order }}</p>
            </div>
            
          </div>
        </div>
        <!-------------------------------------->

        <div class="modal-footer border border-0">
          <button type="button" class="btn bg-white" data-bs-dismiss="modal">
            Close
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["pokemonUrl"],
  data() {
    return { pokemon: {}, url: this.pokemonUrl };
  },

  created() {
    this.getPokemonImageUrl();
  },

  // obtener la data de un pokemon
  methods: {
    async getPokemonImageUrl() {
      try {
        const { data } = await axios.get(this.url);
        this.pokemon = data;
        this.pokemon.abilities = data.abilities;
        this.pokemon.types = data.types;
        this.pokemon.image = data.sprites.other.dream_world.front_default;
      } catch (error) {
        console.error(error);
      }
    },
  },
};
</script>

<style  scoped>
@import url("https://fonts.googleapis.com/css2?family=Nunito:wght@300&display=swap");

.card {
  color: white;
  font-family: "Nunito", sans-serif;
  background: radial-gradient(
    circle,
    rgba(195, 175, 184, 1) 0%,
    rgba(148, 187, 233, 1) 100%
  );
}

.modal-content {
  background: radial-gradient(
    circle,
    rgba(195, 175, 184, 1) 0%,
    rgba(148, 187, 233, 1) 100%
  );
}

img {
  width: 203px;
}
</style>
