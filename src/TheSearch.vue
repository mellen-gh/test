<template>
  <div class="div-search ">
    <div class="form-control center">
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
        <div class="search-box-item nochose" :id="item.id" @click="colorChange(item)"> <div class="box-item">{{ item.name }}</div> </div>
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
  methods: {
    colorChange(element) {
      let SearchIdElement = document.getElementById(element.id)
      if (SearchIdElement.classList.contains('nochose')) {
        SearchIdElement.classList.add("chose");
        SearchIdElement.classList.remove("nochose");
        this.list.push(element)
      }else{
      SearchIdElement.classList.add("nochose");
        SearchIdElement.classList.remove("chose");

      }
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
      {name: "Маша9", id: 13},
      {name: "Вова10", id: 14},
      {name: "Ира11", id: 15},
      {name: "Женя12dddd", id: 16},

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
  max-height: 20vh;
  min-height: 20vh;
  overflow: hidden;
  overflow-y: scroll;
  border:2px solid #2c3e50;
  border-radius: 1em;
  padding: 5px;
}

 .search {
   display: flex;
   margin: 1em;
   width:18%
 }
 .search-box {
   display: flex;
   flex-direction: row;
   flex-flow: wrap;

 }
 .search-box-b {
   padding: 4px;
   width: 33%;
 }
 .chose {
   border: 3px solid #41b883 !important;
   font-weight: 700;
  background-color: #fff;
   border-radius: 7px;
   font-size: 12.5px;
   padding: 3px 0 3px 0 !important;
   box-shadow: 2px 2px 2px 2px #2c3e50;
   color: #425b75!important;
 }
 .search-box-item{
   border: 2px solid #fff;
   font-weight: 700;
   padding-left: 1px;
   padding-right: 1px;
   padding-top:4px;
   padding-bottom:4px;
   border-radius: 8px;
   font-size: 12.5px;
   color: #fff
 }
 .box-item{
   display: inline-block;
   padding: 3px;
 }
</style>