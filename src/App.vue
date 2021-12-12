<template>
  <div id="app">
    <div class="container-fluid">
      <Header class="row" @search="query" />
      <Main :superlista="filmList" :TVList="TVList" class="row" />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/header.vue";
import Main from "./components/Main.vue";
export default {
  name: "App",
  components: {
    Header,
    Main,
  },
  data() {
    return {
      filmList: [],
      querySearch: "",
      TVList: [],
    };
  },
  created() {
    axios
      .get(
        "https://api.themoviedb.org/3/search/movie?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=en-US&query=a&page=1&include_adult=false"
      )
      .then((result) => {
        this.filmList = result.data.results;
      });
    axios
      .get(
        "https://api.themoviedb.org/3/search/tv?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=it-IT&page=1&query=a&include_adult=false"
      )
      .then((result) => {
        this.TVList = result.data.results;
      });
  },

  methods: {
    query(valore) {
      if (valore.length > 0) {
        let array = valore.split(" ").filter((item) => item);
        this.querySearch = array[0];
        if (array.length > 1) {
          for (var i = 1; i < array.length; i++) {
            this.querySearch += "%2B" + array[i];
          }
        }
        axios
          .get(
            "https://api.themoviedb.org/3/search/movie?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=en-US&query=" +
              this.querySearch +
              "&page=1&include_adult=false"
          )
          .then((result) => {
            this.filmList = result.data.results;
          });

        axios
          .get(
            "https://api.themoviedb.org/3/search/tv?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=it-IT&page=1&query=" +
              this.querySearch +
              "&include_adult=false"
          )
          .then((result) => {
            this.TVList = result.data.results;
          });
      } else {
        axios
          .get(
            "https://api.themoviedb.org/3/search/movie?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=en-US&query=a&page=1&include_adult=false"
          )
          .then((result) => {
            this.filmList = result.data.results;
          });
        axios
          .get(
            "https://api.themoviedb.org/3/search/tv?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=it-IT&page=1&query=a&include_adult=false"
          )
          .then((result) => {
            this.TVList = result.data.results;
          });
      }
    },
  },
};
</script>

<style lang="scss">
body {
  background: rgb(27, 27, 27);
  color: white;
}
</style>
