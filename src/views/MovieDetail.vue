<template>
  <div
    class=" flex flex-col items-center justify-between h-full px-12"
    v-if="movie"
  >
    <h2 class=" text-gray-100 my-4 font-bold text-3xl text-center">
      {{ movie.Title }}
    </h2>
    <p class=" mb-4">Initial Release: {{ movie.Year }}</p>
    <img :src="movie.Poster" alt="Movie Poster" class=" rounded" />
    <p class=" my-4 text-center">{{ movie.Plot }}</p>
    <div class=" flex flex-row items-center justify-center mb-4">
      <!-- <div class="flex flex-col items-center bg-gray-400 p-3 rounded mx-3">
        <div class="text-gray-100">{{ movie.Ratings[1].Source }}</div>
        <div>{{ movie.Ratings[1].Value }}</div>
      </div> -->
      <div
        class="flex flex-col items-center bg-gray-400 p-3 rounded text-center"
      >
        <div class="text-gray-100">Director</div>
        <div>{{ movie.Director }}</div>
      </div>
      <div
        class="flex flex-col items-center bg-gray-400 p-3 rounded ml-3 text-center"
      >
        <div class="text-gray-100">Genre</div>
        <div>{{ movie.Genre }}</div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from "@/composables/env.js";
export default {
  setup() {
    const movie = ref({});
    const route = useRoute();

    onBeforeMount(() => {
      fetch(
        `http://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`
      )
        .then((response) => response.json())
        .then((data) => {
          movie.value = data;
        });
    });

    return { movie, route };
  },
};
</script>

<style></style>
