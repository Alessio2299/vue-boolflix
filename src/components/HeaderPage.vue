<template>
  <header>
    <h1>boolflix</h1>
    <div class="search">
      <input type="text" placeholder="Cerca il film o serieTv">
      <button>Cerca</button>
    </div>
  </header>
</template>

<script>
export default {
  name: 'HeaderPage',
  props: {

  }
}
</script>

<style scoped lang="scss">
  header{
    background-color: #000;
    display: flex;
    justify-content: space-between;
    align-items: center;
    h1{
    text-transform: uppercase;
    color: rgb(190, 0, 0);
    padding: 20px;
    }
    .search{
      margin-right: 20px;
      input{
      height: 30px;
      width: 200px;
      margin-right: 10px;
      }
      button{
        height: 30px;
        width: 50px;
      }
    }
  }
</style>
