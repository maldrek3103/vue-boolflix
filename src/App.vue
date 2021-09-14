<template>
  <div id="app">
    <header>
      <Search placeholder="Search a movie/serie" @search="getInput" />
    </header>
  </div>
</template>

<script>
import axios from "axios";
import Search from "../src/components/Search.vue";

export default {
  name: "App",
  data() {
    return {
      movies: [],
      api: {
        key: "695b15da881bf459a0f6ee822a62d1d7",
        base: "https://api.themoviedb.org/3",
      },
    };
  },
  components: {
    Search,
  },
  methods: {
    getInput(query) {
      if (!query) this.movies = [];
      const params = {
        params: {
          query,
          api_key: this.api.key,
          language: "it-IT",
        },
      };

      axios.get(`${this.api.base}/search/movie/`, params).then((res) => {
        this.movies = res.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
</style>
