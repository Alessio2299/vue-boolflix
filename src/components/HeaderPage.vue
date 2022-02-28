<template>
  <header>
    <div class="container-header">
      <h1>boolflix</h1>
      <div class="search">
        <input @keyup.enter="change" type="text" v-model="search" placeholder="Cerca film o serieTv">
        <button @click="change">Cerca</button>
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: 'HeaderPage',
  data(){
    return{
      search: "",
      valueChange: 1
    }
  },
  methods:{
    change(){
      this.valueChange += 1
      this.$emit('textSearch', this.search, this.valueChange)
    }
  }
}
</script>

<style scoped lang="scss">
  header{
    background-color: rgb(26, 26, 26);
    .container-header{
      display: flex;
      justify-content: space-between;
      align-items: center;
      width: 95%;
      margin: auto;
      h1{
      text-transform: uppercase;
      color: rgb(190, 0, 0);
      padding: 20px 0;
      }
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
