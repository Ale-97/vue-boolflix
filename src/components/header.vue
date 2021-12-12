<template>
  <div class="Header d-flex align-items-center justify-content-between">
    <div class="col d-flex align-items-center">
      <img src="../assets/Netflix.png" alt="" />

      <ul class="d-flex">
        <li><a href="">Home</a></li>
        <li><a href="">Serie TV</a></li>
        <li><a href="">Film</a></li>
        <li><a href="">Originali</a></li>
        <li><a href="">Aggiunti di recente</a></li>
        <li><a href="">La mia lista</a></li>
      </ul>
    </div>

    <div class="col-3 d-flex align-items-center justify-content-end">
      <div class="d-flex">
      <input type="text" placeholder="Cerca" v-model="searchString">
      <button @click="$emit('search', searchString)"><i class="fas fa-search"></i></button>
      </div>
      <div>BAMBINI</div>
      <i class="fas fa-bell"></i>
      <div class="d-flex">
          <img src="../assets/Icon-Profile.png" alt="">
          <i class="fas fa-sort-down"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  data(){
    return{
      searchString:"",
    }
  },
};
</script>

<style lang="scss" scoped>
.Header {
  .col {
        img {
            width: 100px;
            margin: 15px 0;
        }
        ul {
            margin: 0;
        li {
            font-size: 15px;
            list-style: none;
            margin: 0 10px;
            a{
              text-decoration: none;
              color: white;
            }
      }
    }
  }

  .col-3{
      &>*{
          margin: 0 10px;
      }
      img{
          margin-right: 4px ;
          width: 24px;
      }
  }
}
</style>
