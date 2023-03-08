<template>
  <div class="home">
<pokemon-list />   

  </div>
</template>

<script>
import PokemonList from '@/components/PokemonList.vue'
// @ is an alias to /src

export default {
  name: 'HomeView',
  components: {
    PokemonList
  }
}
</script>
