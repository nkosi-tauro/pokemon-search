<template>
  <div>
    <link
      rel="stylesheet"
      href="https://cdn.jsdelivr.net/npm/@iconscout/unicons@3.0.6/css/line.css"
    />

    <!-- Pokemon Card -->

    <div
      v-if="pokemon"
      class="min-w-screen min-h-screen bg-yellow-300 flex items-center p-5 lg:p-10 overflow-hidden relative"
    >
      <div
        class="w-full max-w-6xl rounded bg-white shadow-xl p-10 lg:p-20 mx-auto text-gray-800 relative md:text-left"
      >
        <div class="md:flex items-center -mx-10">
          <div class="w-full md:w-1/2 px-10 mb-10 md:mb-0">
            <div class="relative">
              <img
                :src="pokemon.sprites.front_shiny"
                class="w-full relative z-10"
                alt=""
              />
              <div
                class="border-4 border-yellow-200 absolute top-10 bottom-10 left-10 right-10 z-0"
              ></div>
            </div>
          </div>
          <div class="text-center md:w-1/2 px-5">
            <div class="mb-10">
              <h1 class="font-bold uppercase text-2xl mb-5">
                {{ pokemon.name }}
              </h1>
              <p class="text-sm">
                <!-- Lorem ipsum dolor sit, amet consectetur adipisicing, elit. Eos,
                voluptatum dolorum! Laborum blanditiis consequatur, voluptates,
                sint enim fugiat saepe, dolor fugit, magnam explicabo eaque quas
                id quo porro dolorum facilis... -->
              </p>
            </div>
            <div>
              <div class="align-bottom mr-5">
                <h2 class="text-blue-800">Types :</h2>
                <div v-for="(type, idx) in pokemon.types" :key="idx">
                  <h5
                    class="inline-block rounded-full text-white bg-red-400 hover:bg-red-500 duration-300 text-xs font-bold mr-1 md:mr-2 mb-2 px-2 md:px-4 py-1 opacity-90 hover:opacity-100"
                  >
                    {{ type.type.name }}
                  </h5>
                </div>
                <h2 class="text-blue-800">Abilities :</h2>
                <div v-for="(ability, idx) in pokemon.abilities" :key="idx">
                  <h5
                    class="inline-block rounded-full text-white bg-green-400 hover:bg-red-500 duration-300 text-xs font-bold mr-1 md:mr-2 mb-2 px-2 md:px-4 py-1 opacity-90 hover:opacity-100"
                  >
                    {{ ability.ability.name }}
                  </h5>
                </div>
              </div>
              <div class="inline-block align-bottom">
                <!-- <button
                  class="bg-yellow-300 opacity-75 hover:opacity-100 text-yellow-900 hover:text-gray-900 rounded-full px-10 py-2 font-semibold"
                >
                  <i class="mdi mdi-cart -ml-2 mr-2"></i> BUY NOW
                </button> -->
              </div>
            </div>
          </div>
          <div class="w-full md:w-1/2 px-10 mb-10 md:mb-0">
            <div class="relative">
              <img
                :src="pokemon.sprites.back_shiny"
                class="w-full relative z-10"
                alt=""
              />
              <div
                class="border-4 border-yellow-200 absolute top-10 bottom-10 left-10 right-10 z-0"
              ></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { useRoute } from "vue-router";
import { reactive, toRefs } from "vue";
export default {
  setup() {
    const route = useRoute();
    const state = reactive({
      pokemon: null,
    });

    fetch(`https://pokeapi.co/api/v2/pokemon/${route.params.slug}/`)
      .then((res) => res.json())
      .then((data) => {
        console.log(data);
        state.pokemon = data;
      });

    return { ...toRefs(state) };
  },
};
</script>

<style>
@import url(https://cdnjs.cloudflare.com/ajax/libs/MaterialDesign-Webfont/5.3.45/css/materialdesignicons.min.css);
</style>