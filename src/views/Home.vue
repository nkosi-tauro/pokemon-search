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
    v-for="(pokemon, idx) in filteredPokemon" :key="idx"
    class="ml-4 text-2xl text-blue-500">
    <router-link :to="`/pokemon/${urlIdLookup[pokemon.name]}`">{{pokemon.name}}</router-link>
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
      if(!state.pokemonSearch){
        return []
      }
      return state.pokemons.filter((pokemon)=>pokemon.name.includes(state.pokemonSearch))
    }
    fetch("https://pokeapi.co/api/v2/pokemon?limit=500")
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
