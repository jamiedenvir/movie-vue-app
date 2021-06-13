<template>
  <div class="movies-show">
    <h2>{{ movie.title }}</h2>
    <p>Year: {{ movie.year }}</p>
    <p>Director: {{ movie.director }}</p>
    <p>Plot: {{ movie.plot }}</p>
    <br />
    <router-link :to="`/movies/${movie.id}/edit`">Edit</router-link>

    <br />
    <button v-on:click="destroyMovie()">Delete</button>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: () => ({
    movie: {},
  }),
  created: function () {
    axios.get(`/movies/${this.$route.params.id}`).then((response) => {
      this.movie = response.data;
      console.log(response.data);
    });
  },
  methods: {
    destroyMovie: function () {
      if (confirm("Do you really wanna delete this movie?")) {
        axios.delete(`/movies/${this.movie.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/movies");
        });
        console.log("DESTROYED");
      }
    },
  },
};
</script>
