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
    <TheSearch @addList="changeColor"></TheSearch>
    <DragList></DragList>
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
      persons: [],
      value: '',
      maxLengthInCars: 10,
      minLengthInCars: 3,
      display: "Transition",
      order: 1,
      list: [
        {name: "Артём", id: 1},
        {name: "Влад", id: 2},
        {name: "Маша", id: 3},
        {name: "Вова", id: 4},
        {name: "Ира", id: 5},
        {name: "Женя", id: 6},

      ],
      // drag: false,
      oldIndex: '',
      newIndex: ''
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
  methods: {
    alertDel(elem) {
      confirm('Вы действительно хотите удалить из списка участников игрока ' + elem )
    },
    endDrag(evt) {
      this.isDrag = false;
      this.oldIndex = evt.oldIndex;
      this.newIndex = evt.newIndex;

    },
    startDrag() {
      this.isDrag = true;

    },
    randomSort() {

      this.list.sort(function () {
        return Math.random() - 0.5;

      });
    },
    addPlayer() {
        this.$refs.addInput.value = ''
     if (this.value.length <= this.minLengthInCars) {
        this.inputWarning = false
        console.log(1)
       this.$refs.addInput.blur()
      }

    },
    colorChange(element) {
      let SearchIdElement = document.getElementById(element.id)
      if (SearchIdElement.classList.contains('nochose')) {
        SearchIdElement.classList.add("chose");
        SearchIdElement.classList.remove("nochose");

      }else{
        SearchIdElement.classList.add("nochose");
        SearchIdElement.classList.remove("chose");

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

    },
    dragOptions() {
      return {
        animation: 0,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      };
    }
  },
  components: {footerM, DragList,TheSearch}
}
</script>

<style>

</style>
