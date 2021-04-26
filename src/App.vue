<template>
  <div class="row hello">
    <div class="col-2">
      <button class="btn btn-secondary button" @click="sort">
        Как было
      </button>
    </div>


    <h3>TEST DRAG MAF</h3>
    <draggable
        class="list-group"

        tag="transition-group"
        :component-data="{
          tag: 'ul',
          type: 'transition',
          name: 'flip-list'
        }"
        v-model="list"
        v-bind="dragOptions"
        @start="drag = true"
        @end="endDrag"
        item-key="id"
    >

      <template #item="{ element }">
        <li class="list-group-item">

          <strong>{{ element.name }}</strong>  <span>{{ element.id }} </span>
        </li>
      </template>

    </draggable>
    <p><strong>Прошлый:</strong>{{ oldIndex }}</p>
    <p><strong>Новый:</strong> {{ newIndex }}</p>


    <!--    <rawDisplayer class="col-3" :value="list" title="List"/>-->
    <!--    &ndash;&gt;-->
  </div>
</template>

<script>
import draggable from "vuedraggable";

export default {
  name: "transition-example-2",
  display: "Transitions",
  order: 0,
  components: {
    draggable
  },
  data() {
    return {
      list: [
        {name: "Артём", id: 0},
        {name: "Влад", id: 1},
        {name: "Маша", id: 2},
        {name: "Вова", id: 3},
        {name: "Ира", id: 4},
        {name: "Женя", id: 5},

      ],
      drag: false,
      oldIndex: '',
      newIndex: ''
    };
  },
  methods: {
    endDrag(evt) {
      this.drag = false;
      console.log(evt)
      this.oldIndex = evt.oldIndex;
      this.newIndex = evt.newIndex;
    },
    sort() {
      this.list = this.list.sort((a, b) => a.id - b.id);

    }
  },
  computed: {
    dragOptions() {
      return {
        animation: 200,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      };
    }
  }
};
</script>

<style lang="scss">
strong {
  display: inline-block;
}

.sortable {

}

.list-group {
  padding-inline-start: 0px;
}

#app {
  padding: 4em;
}

body {
  background-color: rgb(231, 231, 231);
}

#app {
  background-color: rgb(231, 231, 231);
}

.button {
  margin-top: 35px;
}

.flip-list-move {
  transition: transform 0.5s;
}

.no-move {
  transition: transform 0s;
}

.ghost {
  opacity: 0.5;
  background: #c8ebfb;
}

.list-group {
  min-height: 20px;
}

.list-group-item {

  cursor: move;
}



.list-group-item i {
  cursor: pointer;
}

.sortable-chosen {
  opacity: 0;
}

.list-group-item {
  width: 100%;
  background-color: #fff;
  padding: 1em;
  list-style-type: none;
  margin-bottom: 2px;
  span {
    float: right;
  }
}
.sortable-chosen {
  opacity: 0.4;
}
.sortable-chosen {
  transition: transform 0.5s;
}
.ghost {
  border-left: 6px solid #42b983;
  box-shadow: 10px 10px 5px -1px rgba(0,0,0,0.14);
  opacity: .7;

  &::before{
    content: " ";

    position: absolute;
    width: 20px;
    height: 20px;
    margin-left: -50px;
    background-image: url("../public/123.svg") ;
  }
}
</style>
