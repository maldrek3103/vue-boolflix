<template>
  <div id="app">
    <header>
      <Search placeholder="Search a movie/serie" @search="getInputs" />
    </header>
    <main>
      <ul v-for="item in mergedResult" :key="item.id">
        <li>{{ item.title || item.name }}</li>
        <li>{{ item.original_title || item.original_name }}</li>
        <li>{{ item.original_language }}</li>
        <li>{{ item.vote_average }}</li>
      </ul>
    </main>
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
      series: [],
      api: {
        key: "695b15da881bf459a0f6ee822a62d1d7",
        base: "https://api.themoviedb.org/3",
      },
    };
  },
  computed: {
    mergedResult() {
      return [...this.movies, ...this.series];
    },
  },
  components: {
    Search,
  },
  methods: {
    getInputs(query) {
      if (!query) {
        this.movies = [];
        this.series = [];
        return;
      }

      this.fetchApi(query, "search/movie/", "movies");
      this.fetchApi(query, "search/tv/", "series");
    },
    fetchApi(query, endpoint, entity) {
      const params = {
        params: {
          query,
          api_key: this.api.key,
          language: "it-IT",
        },
      };
      axios.get(`${this.api.base}/${endpoint}`, params).then((res) => {
        this[entity] = res.data.results;
      });
    },
  },
};
</script>

<style lang="scss">
</style>
