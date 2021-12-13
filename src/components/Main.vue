<template>
  <div class="Main">
    <div class="col-12">
      <h3>ORIGINALI NETFLIX</h3>
      <h5>Film</h5>
    </div>
    <!-- costruisce la lista di film -->
    <div class="col-12">
      <div class="row">
        <Card
          class="col-2"
          v-for="film in FilmList"
          :key="film.id"
          :backgroundImage="film.poster_path"
          :title="film.title"
          :originalTitle="film.original_title"
          :language="film.original_language"
          :vote="film.vote_average"
        />
      </div>
    </div>

    <div class="col-12">
      <h5>Serie TV</h5>
    </div>

    <!-- costruisce la lista di serie tv -->
    <div class="col-12">
      <div class="row">
        <Card
          class="col-2"
          v-for="tvShow in TVList"
          :key="tvShow.id"
          :backgroundImage="tvShow.poster_path"
          :title="tvShow.name"
          :originalTitle="tvShow.original_name"
          :language="tvShow.original_language"
          :vote="tvShow.vote_average"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Card from "./Card.vue";
export default {
  name: "Main",
  components: {
    Card,
  },
  props: {
    FilmList: Array,
    TVList: Array,
  },
};
</script>

<style lang="scss" scoped>
.Main {
  h3 {
    margin: 20px 0;
  }

  .row {
    padding-bottom: 20px;
    overflow: auto;
    flex-wrap: nowrap;
    margin-bottom: 50px;
    &::-webkit-scrollbar-track {
      border-radius: 20px;
      background: rgba($color: black, $alpha: 0.3);
    }
    &::-webkit-scrollbar {
      height: 6px;
    }
    &::-webkit-scrollbar-thumb {
      background-color: red;
      border-radius: 20px;
    }
  }
}
</style>
