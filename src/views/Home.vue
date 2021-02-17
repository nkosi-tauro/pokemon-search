<template>
  <div class="w-full flex justify-center">
    <input 
    v-model="pokemonSearch"
    class="mt-10 p-2 border-blue-600 border-2"
    type="text" 
    placeholder="Enter Pokemon here" />
  </div>
  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div 
    v-for="(pokemon, idx) in pokemons" :key="idx"
    class="ml-4 text-2xl text-blue-500">
    {{pokemon.name}}
    </div>
  </div>
</template>

<script>
import { computed, reactive, toRefs } from "vue";

export default {
  name: "Home",
  setup() {
    const state = reactive({
      pokemons: [],
      urlIdLookup: {},
      pokemonSearch: "",
      filteredPokemon: computed(() => updatePokemon())
    });

    function updatePokemon(){
      
    }
    fetch("https://pokeapi.co/api/v2/pokemon?offset=0")
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        state.pokemons = data.results;
        state.urlIdLookup = data.results.reduce(
          (acc, cur, idx) => (acc = { ...acc, [cur.name]: idx + 1 }),
          {}
        );
      });

    return { ...toRefs(state) };
  },
};
</script>
