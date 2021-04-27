<template>
  <div class="div-search ">
    <div class="center">
    <input
        v-model="search"
        type="search"
        class="search"
        placeholder="Имя игрока"
        />
    </div>
    <div class="container">
      <div class="search-box">
      <div v-for="item in searchHandler" :key="item.id" class="search-box-b">
        <div class="search-box-item"> <div class="box-item">{{ item.name }}</div> </div>
      </div>
      </div>
    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      search: '',
      persons: []
    }
  },
  created() {
    this.persons = [
      {name: "Артём", id: 1},
      {name: "Влад", id: 2},
      {name: "Маша", id: 3},
      {name: "Вова", id: 4},
      {name: "Ира", id: 5},
      {name: "Женя", id: 6},
      {name: "Артём7", id: 7},
      {name: "Влад8", id: 8},
      {name: "Маша9", id: 9},
      {name: "Вова10", id: 10},
      {name: "Ира11", id: 11},
      {name: "Женя12dddd", id: 12},
      {name: "Маша9", id: 9},
      {name: "Вова10", id: 10},
      {name: "Ира11", id: 11},
      {name: "Женя12dddd", id: 12},

    ];
    console.log(this.persons)
  },
  computed: {
    searchHandler() {
      return this.persons.filter(element => {
        return element.name.toLowerCase().includes(this.search.toLowerCase())
      });

    }
  }
}
</script>

<style scoped>
.container{
  max-height: 220px;
  overflow: hidden;
  overflow-y: scroll;
  border:2px solid #2c3e50;
  border-radius: 1em;
}

 .search {
   display: flex;
   margin: 1em;
 }
 .search-box {
   display: flex;
   flex-direction: row;
   flex-flow: wrap;

 }
 .search-box-b {
   padding: 6px;
   width: 33%;
 }
 .search-box-item {
   border: 1px solid #fff;

   border-radius: 5px;
   font-size: 12.5px;
   color: #fff
 }
 .box-item{
   display: inline-block;
   padding: 10px;
 }
</style>