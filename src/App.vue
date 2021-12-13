<template>
  <div id="app">
    <div class="container-fluid">
      <!-- Contiene la navbar con la barra di ricerca -->
      <Header class="row" @search="query" />
      <!-- Contenuto principale della pagina -->
      <Main :FilmList="filmList" :TVList="TVList" class="row" />
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
      filmList: [],//Lista dei Film aquisiti 
      TVList: [],//Lista delle serie tv aquisite
      querySearch: "",//Viene popolata con il valore che verra messo nella query della chiamata per la ricerca
    };
  },
  created() {
    //Prima chiamata per visualizzare del contenuto alla creazione della pagina
  this.query("") //film e serie tv più popolari
   },

  methods: {
    //questa funzione verra chiamata ogni volta che si cercherà qualcosa e restituira delle nuove liste in tvList e filmList
    query(valore) {
      if (valore.length > 0) {
        let array = valore.split(" ").filter((item) => item);//serve  per togliere gli spazi e restituirmi un array con le parole inviate dalla ricerca
        this.querySearch = array[0];
        if (array.length > 1) {//se array e popolato da una sola parola all'ora è pronta per la ricerca 
          for (var i = 1; i < array.length; i++) {//se ci sono più valori all'interno allora lo codifico nel modo correto per inserirlo nella mia chiamata al server
            this.querySearch += "%2B" + array[i];
          }
        }
        axios
          .get(//chiamata per una lista film in base alla ricerca
            "https://api.themoviedb.org/3/search/movie?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=en-US&query=" +
              this.querySearch +
              "&page=1&include_adult=false"
          )
          .then((result) => {
            this.filmList = result.data.results;
          });

        axios
          .get(//chiamata per una lista di serie tv in base alla ricerca
            "https://api.themoviedb.org/3/search/tv?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=it-IT&page=1&query=" +
              this.querySearch +
              "&include_adult=false"
          )
          .then((result) => {
            this.TVList = result.data.results;
          });
      } else {//se "valore" non ha un contenuto la chiamata restituira la lista generica iniziale
        axios
          .get(//lista film popolari
        "https://api.themoviedb.org/3/movie/popular?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=en-US&page=1&include_adult=false"
          )
          .then((result) => {
            this.filmList = result.data.results;
          });
        axios
          .get(//lista serie tv popolari
        "https://api.themoviedb.org/3/tv/popular?api_key=f3e38786a7566bd6e81d253fd6cbc4b4&language=it-IT&page=1&include_adult=false"
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
// sfondo e colore  generico della pagina
body {
  background: rgb(27, 27, 27);
  color: white;

&::-webkit-scrollbar {
  width: 6px; 
  margin-left:10px ;
}
&::-webkit-scrollbar-thumb {
  background-color: red;    
  border-radius: 20px;       
}
}


</style>
