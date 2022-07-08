<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://vuejs.org/api/sfc-script-setup.html#script-setup
import PokemonCard from "./components/PokemonCard.vue";
import SearchBar from "./components/SearchBar.vue";
import api from "./services/api";

export default {
  name: "Pokedex",
  components: {
    PokemonCard,
    SearchBar,
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      search: ''
    };
  },
  //Função é executada quando a página é criada
  created: function () {
    api.get("pokemon?limit=151&offset=0").then((response) => {
      this.pokemons = response.data.results;
      this.filteredPokemons = response.data.results;
    });
  },
  methods: {
    searchPokemons: function (search) {
      this.filteredPokemons = this.pokemons;
      if (this.search == '' || this.search == ' ') {
        this.filteredPokemons = this.pokemons;
      } else {
        this.filteredPokemons = this.pokemons.filter((pokemon) =>
          pokemon.name.includes(search)
        );
      }
    }
  }
};
</script>

<template>
  <section class="body">
    <SearchBar v-on:change="searchPokemons" />
    <div class="listPokemon">
      <div v-for="(pokemon, index) in pokemons">
        <PokemonCard :index="index + 1" :name="pokemon.name" :url="pokemon.url" />
      </div>
    </div>
  </section>
</template>

<style>
* {
  border: 0;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.body {
  width: 100%;
  min-height: 100vh;
  background-color: #ededed;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.listPokemon {
  width: 100%;
  height: 98%;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  /* justify-content: center; */
}
</style>
