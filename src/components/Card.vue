<template>
  <div  v-if="this.background != null"  class="Card" >
    <div class="container-card">
    <img :src="IMG" alt="not found">
    <div class="testo">
      <div v-if="this.title !== this.originalTitle">
        <div> {{this.title}}</div>
        <div>{{this.originalTitle}}</div>
      </div>
      <div v-else>
        <div> {{this.title}}</div>
      </div>
     <div> {{this.language}}</div>
     <div> {{this.vote}}</div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: "Card",
  data(){
    return{
      IMG:"http://image.tmdb.org/t/p/w500/"+this.background,
    }
  },

  props:{
      background:String,
      title:String,
      originalTitle:String,
      language:String,
      vote:Number,

  },

};
</script>

<style lang="scss" scoped>

  .container-card{
    position: relative;
    img{
      width:  100%;
    }
    .testo{
      position:absolute;
      top: 0;
      height: 100%;
      width: 100%;
      display:flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      background-color: rgba($color: #000000, $alpha: 0.4);
      font-weight: bold;
      text-align: center;

      opacity: 0;
      &:hover{
        opacity: 1;
  
      }
    }

}
</style>
