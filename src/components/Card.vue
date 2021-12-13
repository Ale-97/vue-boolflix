<template>

  <div v-if="this.backgroundImage != null" class="Card">

    <div class="container-card">
      <!--Immagine di sfondo della card  -->
      <img :src="IMG" alt="not found" />
      <!-- Contenuto della card  -->
      <div class="contentCard">
        <!-- Restituisceil titolo e il titolo originale solo se sono diversi nel caso contrario restitusce solo il titolo -->
        <div v-if="this.title !== this.originalTitle">
          <div>{{ this.title }}</div>
          <div>{{ this.originalTitle }}</div>
        </div>
        <div v-else>
          <div>{{ this.title }}</div>
        </div>
      <!-- restituisce l'immagine con la bandiera corrispondente alla lingua del film-->
          <img class="flag" :src="flag(this.language)" alt="" />
      <!-- restituisce delle stelle che corrispondo al voto del film o della serie tv-->
        <div class="d-flex">
          <!-- ciclo con un dato di 5 elementi per generare le mie 5 icone di stelle -->
          <div v-for="element in this.numberStar" :key="element.id">
            <!-- se il voto è superiore al numero di "numberStar" in quel momento restituirà un icona con la classe star che colorerà la stella di giallo -->
            <i v-if="star() >= element" class="fas fa-star star"></i>
            <i v-else class="far fa-star"></i>
          </div>
        </div>

      </div>

    </div>

  </div>
</template>

<script>
export default {
  name: "Card",
  data() {
    return {
      IMG: "http://image.tmdb.org/t/p/w500/" + this.backgroundImage,
      icon: "",
      numberStar: [1, 2, 3, 4, 5],// Serve per ciclare e creare le stelle di valutazione, la numerazione non è casuale , il numero 
    };                            //coincide sia con il numero della stella nella creazione sia con il suo valore così che
  },                              // poi possa verificare che il valore del voto sia superiore alla stella cdreata in quel momento

  props: {
    backgroundImage: String,
    title: String,
    originalTitle: String,
    language: String,
    vote: Number,
  },
  methods: {
    star() {//restituisce il valore del voto approssimato per eccesso
      let numberStar = this.vote / 2;
      this.icon = Math.ceil(numberStar);
      return this.icon;
    },
    // restituisce il percorso per l'immagine della bandiera
    flag(flag){
      return require("../assets/flags/"+ flag + ".png")
    }
  },
};
</script>

<style lang="scss" scoped>
.container-card {
  position: relative;
  img {
    width: 100%;
  }
  .contentCard {
    position: absolute;
    top: 0;
    height: 100%;
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    background-color: rgba($color: #000000, $alpha: 0.4);
    font-weight: bold;
    text-align: center;
    opacity: 0;
    &:hover {
      opacity: 1;
    }

    .flag {
      width: 20px;
      margin: 10px 0;
    }

    .star {
      color: gold;
    }
  }
}
</style>
