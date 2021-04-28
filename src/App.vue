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
      <button class="button-add" :persons="persons" @click="addPlayer"><span>Добавить</span></button>
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
      minLengthInCars: 3
    }
  },
  methods: {
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
