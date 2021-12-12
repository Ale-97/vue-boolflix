<template>
  <div class="Main">
    <div class="col-12">
      <h3>ORIGINALI NETFLIX</h3>
      <h5>Film</h5>
    </div>
    <div class="col-12">
      <div class="row">
        <Card
          class="col-2"
          v-for="film in superlista"
          :key="film.id"
          :background="film.poster_path"
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
    <div class="col-12">
      <div class="row">
        <Card
          class="col-2"
          v-for="tvShow in TVList"
          :key="tvShow.id"
          :background="tvShow.poster_path"
          :title="tvShow.name"
          :originalTitle="tvShow.original_title"
          :language="tvShow.original_name"
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
    superlista: Array,
    TVList:Array
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
  }
}
</style>
