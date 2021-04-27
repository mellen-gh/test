<template>
  <div class="row hello">
    <div>
      <button class="btn primary btn-random" @click="randomSort">
        <div></div>
      </button>

      <div class="player-list"><h3>Список игроков</h3></div>

    </div>
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

      <template #item="{ element, index }">
        <li class="list-group-item li-drag">

          <div class="list-index">{{ index + 1 }}</div>
          <div class="list-elem"><strong>{{ element.name }}</strong></div>
          <div class="list-elem-del" @click="alertDel"><img src="../public/Delete.svg" alt=""></div>
        </li>
      </template>

    </draggable>
    <!--    <p><strong>Прошлый:</strong>{{ oldIndex }}</p>-->
    <!--    <p><strong>Новый:</strong> {{ newIndex }}</p>-->


    <!--    <rawDisplayer class="col-3" :value="list" title="List"/>-->
    <!--    &ndash;&gt;-->
  </div>
</template>

<script>
import draggable from "vuedraggable";

document.addEventListener('contextmenu', event => event.preventDefault());
export default {
  name: "transition-example",
  display: "Transition",
  order: 1,
  components: {
    draggable
  },
  data() {
    return {
      list: [
        {name: "Артём", id: 1},
        {name: "Влад", id: 2},
        {name: "Маша", id: 3},
        {name: "Вова", id: 4},
        {name: "Ира", id: 5},
        {name: "Женя", id: 6},

      ],
      drag: false,
      oldIndex: '',
      newIndex: ''
    };
  },

  methods: {
    alertDel() {
      alert(123)
    },
    endDrag(evt) {
      this.drag = false;
      this.oldIndex = evt.oldIndex;
      this.newIndex = evt.newIndex;
    },

    randomSort() {
      this.list.sort(function () {
        return Math.random() - 0.5;
      });
    }
  },
  computed: {
    dragOptions() {
      return {
        animation: 300,
        group: "description",
        disabled: false,
        ghostClass: "ghost"
      };
    }

  }
};
</script>

<style lang="scss" scoped>
.player-list {
  display: inline-block;
  text-align: center !important;
  width: 100%;
  z-index: 0;
  h3 {
    margin-bottom: 5px;
  }
}

.btn-random {
  position: absolute;
  z-index: 2;
  padding: 8px;
  background-color: #5c7ca1 !important;
  box-shadow: 0px 0px 10px 7px #2c3e50;
  border: 3px solid #41B883;
  display: inline-block;
  &:after{
    content: "";
    background: #2c3e50;
    display: block;
    position: absolute;
    padding-top: 300%;
    padding-left: 350%;
    margin-left: -20px !important;
    margin-top: -120%;
    opacity: 0;
    color: #2c3e50 !important;
    transition: all 0.8s
  }

  div {
    background: url("../public/Swap.svg");
    width: 24px;
    color: #425b75;
    height: 24px;
  }
}

li {
  border-top-left-radius: 20px;
  border-bottom-left-radius: 20px;

  div.list-index {
    display: inline-block;
    border-right: 2px solid #425b75;
    padding: 0.3em;
    padding-left: 16px;
    width: 40px

  }

  div.list-elem {
    display: inline-block;
    padding-left: 12px;
  }
}

strong {
  display: inline-block;
}

.list-elem-del {
  display: inline-block;
  float: right;
  padding-top: 0.35em;
  padding-right: 10px;
  padding-left: 10px;
  border-left: 2px solid #425b75;
  background-color: #41B883;
  cursor: default;

}

.flip-list-move {
  transition: transform 0.5s;
}

.no-move {
  transition: transform 0s;
}

.list-group {
  padding-inline-start: 0;
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

.ghost .list-index {
  //border-right: 6px solid #42b983;
  border-bottom-left-radius: 20px;
  border-top-left-radius: 20px;
  background-color: #41B883;
  box-shadow: 10px 10px 5px -1px rgba(0, 0, 0, 0.14);
  opacity: 0.8;

  //&::after{
  //  content: " ";
  //  right: 0.6em;
  //  position: absolute;
  //  width: 20px;
  //  height: 20px;
  //  float:right;
  //  opacity: 1;
  //  background-image: url("../public/Swap.svg") ;
  //}
}
</style>
