<template>
  <div class="movies-index">
    <h2>Movies</h2>
    Search by title:
    <input type="text" v-model="titleFilter" placeholder="Search" />
    <br />
    <br />

    <!-- Cards in a grid -->
    <div class="row">
      <div class="col-sm-6">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Back to the Future</h5>
            <img
              src="https://img.i-scmp.com/cdn-cgi/image/fit=contain,width=425,format=auto/sites/default/files/styles/768x768/public/d8/images/methode/2019/04/19/72d249d6-61b2-11e9-b745-17e2afcf325c_image_hires_185916.jpg?itok=CVcasVGm&v=1555671562"
              alt=""
            />
            <p class="card-text">Doc!</p>
            <a href="movies/2" class="btn btn-outline-info">Learn About Back to the Future</a>
          </div>
        </div>
      </div>
      <div class="col-sm-6">
        <div class="card">
          <div class="card-body">
            <h5 class="card-title">Jurassic Park</h5>
            <img
              src="https://www.thewrap.com/wp-content/uploads/2018/06/MV5BNTE3ODQ4NjkwNV5BMl5BanBnXkFtZTcwMzg4OTI3OA@@._V1_SY1000_CR0013481000_AL_.jpg"
              alt=""
            />
            <p class="card-text">Must go faster!</p>
            <a href="movies/1" class="btn btn-outline-danger">Learn About Jurassic Park</a>
          </div>
        </div>
      </div>
    </div>
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
