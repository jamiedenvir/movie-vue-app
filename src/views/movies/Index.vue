<template>
  <div class="movies-index">
    <h2>Movies</h2>
    Search by title:
    <input type="text" v-model="titleFilter" placeholder="Search" />
    <div v-for="movie in filterBy(movies, titleFilter, 'title')" v-bind:key="movie.id">
      <router-link :to="`/movies/${movie.id}`">
        <h4>{{ movie.title }} ({{ movie.year }})</h4>
      </router-link>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";
import Vue2Filters from "vue2-filters";

export default {
  mixins: [Vue2Filters.mixin],
  data: function () {
    return {
      movies: [],
      titleFilter: "",
    };
  },
  created: function () {
    axios.get("/movies").then((response) => {
      console.log("Movies array", response.data);
      this.movies = response.data;
    });
  },
  methods: {},
};
</script>
