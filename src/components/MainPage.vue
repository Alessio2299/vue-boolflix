<template>
  <main>
    <div class="film">
      <h2>film</h2>
      <div class="container-film">
        <div class="button">
          <i class="next fas fa-chevron-circle-right"></i>
          <i class="prev fas fa-chevron-circle-left"></i>
        </div>
        <div class="card" v-for="card in 6" :key="card">
          <img src="https://www.staynerd.com/wp-content/uploads/Annihilation_Vertical-MAIN_PRE_ITA.jpg" alt="Film">
        </div>
      </div>
    </div>
    <div class="serieTv">
      <h2>serie Tv</h2>
      <div class="container-serieTv">
        <div class="button">
          <i class="next fas fa-chevron-circle-right"></i>
          <i class="prev fas fa-chevron-circle-left"></i>
        </div>
        <div class="card" v-for="card in 6" :key="card">
          <img src="https://www.staynerd.com/wp-content/uploads/Annihilation_Vertical-MAIN_PRE_ITA.jpg" alt="Film">
        </div>
      </div>
    </div>
  </main>
</template>

<script>
  export default {

  }
</script>

<style scoped lang="scss">
  main{
    height: calc(100% - 77px);
    background-color: rgb(26, 26, 26);
    padding-top: 30px;
    .film,
    .serieTv{
      height: 450px;
      width: 95%;
      margin: auto;
      padding-bottom: 40px;
      color: #fff;
      h2{
        text-transform: uppercase;
        height: 30px;
        padding: 5px;
        margin-bottom: 10px;
      }
      .container-film,
      .container-serieTv{
        display: flex;
        height: calc(100% - 30px);
        position: relative;
        .next,
        .prev{
          position: absolute;
          border-radius: 50%;
          top: 50%;
          transform: translateY(-50%);
          font-size: 35px;
          color: rgba(255, 255, 255, 0.6);
          cursor: pointer;
          &:hover{
            transform: translateY(-50%) scale(1.2);
          }
        }
        .next{
          right: 10px;
        }
        .prev{
          left: 10px;
        }
        .card{
        width: calc(100% / 6);
        height: 100%;
        background-color: hotpink;
        border: 2px solid rgb(26, 26, 26);
          img{
            width: 100%;
            height: 100%;
            object-fit: cover;
          }
        }
      }
    }
  }
</style>