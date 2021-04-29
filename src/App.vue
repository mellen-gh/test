<template>

  <div class="container card">
    <div class="form-control center" :class="inputWarning ? '' : 'invalid'" @submit.prevent="">
      <input
          type="text"
          class="inputAdd"
          ref="addInput"
          id="addPlayer"
          @input="assertMaxChars()"
          v-model="value"/>
      <button class="button-add" @click="addPlayer"><span>Добавить</span></button>
    </div>
    <TheSearch @addList="colorChange" :persons="persons" ></TheSearch>
    <DragList  v-if="this.list.length > 0" :list="list" @remove="removeFromList" @randomSort="randomSort"></DragList>
    <footerM></footerM>
  </div>

</template>

<script>
// import axios from 'axios'
import footerM from "@/footerM";
import DragList from "@/DragList";
import TheSearch from "./TheSearch";

export default {
  data() {
    return {
      inputWarning: true,
      search: '',
      persons: [
        {name:'Влад', id: 1},
        {name:'Артём', id: 2},
        {name:'Вова', id: 3},
        {name:'Ира', id: 4},
        {name:'Женя', id: 5},
        {name:'Рома', id: 6},
        {name:'Арсений', id: 7},
        {name:'Милена', id: 8},
        {name:'Оля', id: 9},
        {name:'Тимур', id: 10},
        {name:'Олег', id: 11},
        {name:'Павел', id: 12},
        {name:'Игнат', id: 13},
      ],
      list: [],
      value: '',
      maxLengthInCars: 10,
      minLengthInCars: 3
    }
  },
  methods: {
    removeFromList($event) {
      const idToRemove = $event.id
      this.list = this.list.filter((item) => item.id !== idToRemove);
      let SearchIdElement = document.getElementById($event.id)
      SearchIdElement.classList.add("nochose");
      SearchIdElement.classList.remove("chose");
      console.log($event)
      console.log(this.list)

    },
    randomSort() {

      this.list.sort(function () {
        return Math.random() - 0.5;

      });
    },
    colorChange(element) {
      let SearchIdElement = document.getElementById(element.id)
      const idToRemove = element.id
      if (SearchIdElement.classList.contains('nochose')) {
        SearchIdElement.classList.add("chose");
        SearchIdElement.classList.remove("nochose");
        this.list.push(element)

        console.log(this.list)

      }else{
        SearchIdElement.classList.add("nochose");
        SearchIdElement.classList.remove("chose");
        console.log(element)
        this.list = this.list.filter((item) => item.id !== idToRemove);
      }
    },
    addPlayer() {
        this.$refs.addInput.value = ''
     if (this.value.length <= this.minLengthInCars) {
        this.inputWarning = false
        console.log(1)
       this.$refs.addInput.blur()

      }

    },

    assertMaxChars: function () {
      if (this.value.length >= this.maxLengthInCars) {
        this.value = this.value.substring(0,this.maxLengthInCars);
      }

    }
  },
  computed: {
    searchHandler() {
      return this.persons.filter(element => {
        return element.name.toLowerCase().includes(this.search.toLowerCase())
      });

    }
  },
  components: {footerM, DragList,TheSearch}
}
</script>

<style>

</style>
