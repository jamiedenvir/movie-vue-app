<template>
  <div class="home">
    <h2>New Movie</h2>
    <input type="text" v-model="newMovieTitle" placeholder="Title" />
    <br />
    <input type="text" v-model="newMovieYear" placeholder="Year" />
    <br />
    <input type="text" v-model="newMoviePlot" placeholder="Plot" />
    <br />
    <input type="text" v-model="newMovieDirector" placeholder="Director" />
    <br />
    <input type="text" v-model="newMovieEnglish" placeholder="English?" />
    <br />

    <button v-on:click="createMovie()">Add Movie</button>

    <div v-for="movie in movies" :key="movie.id">
      <button v-on:click="showInfo(movie)">More Info</button>
      <h3>Title: {{ movie.title }}</h3>
      <p>Year: {{ movie.year }}</p>
      <p>Plot: {{ movie.plot }}</p>
      <p>Director: {{ movie.director }}</p>
    </div>
    <dialog id="movie-details">
      <form method="dialog">
        <h1>Movie Info!</h1>
        <p>Title: {{ currentMovie.title }}</p>
        <p>Year: {{ currentMovie.year }}</p>
        <p>Plot: {{ currentMovie.plot }}</p>
        <p>Director: {{ currentMovie.director }}</p>
        <button>Close</button>
      </form>
    </dialog>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      movies: [],
      currentMovie: {},
      newMovieTitle: "",
      newMovieYear: "",
      newMoviePlot: "",
      newMovieDirector: "",
      newMovieEnglish: "",
    };
  },
  created: function () {
    this.indexMovies();
  },
  methods: {
    indexMovies: function () {
      axios.get("http://localhost:3000/movies").then((response) => {
        console.log(response.data);
        this.movies = response.data;
      });
    },
    createMovie: function () {
      var params = {
        title: this.newMovieTitle,
        year: this.newMovieYear,
        plot: this.newMoviePlot,
        director: this.newMovieDirector,
        english: this.newMovieEnglish,
      };
      axios
        .post("http://localhost:3000/movies", params)
        .then((response) => {
          console.log("You've done it!", response.data);
          this.movies.push(response.data);
          this.newMovieTitle = "";
          this.newMovieYear = "";
          this.newMoviePlot = "";
          this.newMovieDirector = "";
          this.newMovieEnglish = "";
        })
        .catch((error) => {
          console.log(error.response.data.errors);
        });
    },
    showInfo: function (movie) {
      this.currentMovie = movie;
      console.log(movie);
      document.querySelector("#movie-details").showModal();
    },
  },
};
</script>
