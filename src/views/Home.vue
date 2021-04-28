<template>
  <div class="home">
    <div class=" relative">
      <router-link to="/movie/tt7286456">
        <img
          class=" w-full h-96 object-cover relative z-0"
          src="https://variety.com/wp-content/uploads/2019/04/joker-trailer.jpg?w=1000"
          alt="Featured Poster"
        />
        <div
          class=" absolute left-0 right-0 bottom-0 bg-black bg-opacity-50 p-5 "
        >
          <h3 class=" text-gray-100 mb-4 font-bold">Joker</h3>
          <p class=" text-gray-200">
            In Gotham City, mentally troubled comedian Arthur Fleck is
            disregarded and mistreated by society. He then embarks on a downward
            spiral of revolution and bloody crime. This path brings him
            face-to-face with his alter-ego: the Joker.
          </p>
        </div>
      </router-link>
    </div>
    <form
      @submit.prevent="searchMovies"
      class=" flex flex-col justify-center p-4 items-center"
    >
      <input
        type="text"
        placeholder="Search for a movie"
        class="rounded text-center border-none w-full transition-all bg-gray-50 focus:shadow-lg"
        v-model="search"
      />
      <input
        type="submit"
        value="Search"
        class=" py-3 px-8 rounded mt-2 outline-none bg-gray-700 text-gray-50 w-full active:bg-gray-600"
      />
    </form>

    <div class=" flex flex-wrap items-center justify-center">
      <div
        v-for="movie in movies"
        :key="movie.imdbID"
        class=" mx-4 mb-4 bg-gray-600 flex flex-col justify-center items-center rounded relative w-40"
      >
        <router-link :to="'/movie/' + movie.imdbID">
          <img
            :src="movie.Poster"
            alt="Movie Poster"
            class="  block object-cover w-full h-64 rounded-t"
          />
          <div
            class=" absolute top-2 left-2 bg-gray-400 p-2 rounded shadow-lg capitalize"
          >
            {{ movie.Type }}
          </div>

          <div
            class="  p-4 h-24 w-full flex flex-col items-left justify-center text-sm "
          >
            <div class=" text-gray-400">
              {{ movie.Year }}
            </div>
            <h3 class=" font-bold text-gray-50">
              {{ movie.Title }}
            </h3>
          </div>
        </router-link>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/composables/env.js";
export default {
  setup() {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if (search.value != "") {
        fetch(`http://www.omdbapi.com/?apikey=${env.apikey}&s=${search.value}`)
          .then((response) => response.json())
          .then((data) => {
            movies.value = data.Search;
            search.value = "";
          });
      }
    };

    return { search, movies, searchMovies };
  },
};
</script>

<style></style>
