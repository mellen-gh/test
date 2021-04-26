<template>
  <div class="row">
    <div class="col-2">
      <button class="btn btn-secondary button" @click="sort">
        Как было
      </button>
    </div>

    <div class="col-6">
      <h3>TEST DRAG MAF</h3>
      <draggable
          class="list-group"
          tag="transition-group"
          :component-data="{
          tag: 'ul',
          type: 'transition-group',
          name: !drag ? 'flip-list' : null
        }"
          v-model="list"
          v-bind="dragOptions"
          @start="drag = true"
          @end="endDrag"
          item-key="id"
      >
        <template #item="{ element }">
          <li class="list-group-item">

            {{element.id}}  {{ element.name }}
          </li>
        </template>
      </draggable>
    </div>

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
      drag: false
    };
  },
  methods: {
    endDrag() {
      this.drag = false;
      console.log(this.list)
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

<style>
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
  padding: 8px;
  border: 1px solid black;
  margin: 2px;
  cursor: move;
}

.list-group-item i {
  cursor: pointer;
}
</style>
