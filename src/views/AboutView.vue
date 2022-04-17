<template>
  <div class="about">
    <div
      v-if="pokemon"
      class="
        w-3/12
        m-auto
        bg-purple-100
        mt-4
        shadow-2xl
        flex
        justify-center
        flex-col
        items-center
        rounded-md
        p-4
      "
    >
      <h3 class="text-2xl text-green-900 uppercase font-semibold">
        {{ pokemon.name }}
      </h3>
      <div class="flex justify-center">
        <img class="w-48" :src="pokemon.sprites.front_shiny" alt="" />
        <img class="w-48" :src="pokemon.sprites.back_shiny" alt="" />
      </div>
      <h3 class="text-yellow-700 mb-2 font-semibold">Types</h3>
      <div v-for="(type, idx) in pokemon.types" :key="idx">
        <h5 class="text-blue-500 first-letter:uppercase">
          {{ type.type.name }}
        </h5>
      </div>
    </div>
    <div class="flex justify-center">
      <router-link
        class="
          flex
          justify-center
          items-center
          text-1xl text-white
          font-bold
          mt-10
          rounded-full
          bg-red-500
          w-2/12
          h-8
          hover:bg-red-600
          active:bg-red-700
          focus:ring focus:ring-red-300
        "
        to="/"
      >
        Go Back
      </router-link>
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
