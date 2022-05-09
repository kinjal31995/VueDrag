<template>
  <div class="container">
    <Navbar />
    <div class="row">
      <div class="col form-inline">
        <b-input
          v-model="newTask"
          placeholder="Add New Task"
          @keyup:enter="add"
        >
        </b-input>
        <b-button @click="add" variant="primary" class="ml-3">Add</b-button>
      </div>
    </div>

    <div class="row mt-3">
      <div class="col-3">
        <div class="p-2 alert alert-secondary">
          <h3>Tasks</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrTasks"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="element in arrTasks"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 alert alert-secondary">
          <h3>In Progress</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrInProgress"
            group="tasks"
          >
            <div
              class="list-group-item"
              v-for="element in arrInProgress"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>

      <div class="col-3">
        <div class="p-2 alert alert-success">
          <h3>Done</h3>
          <draggable
            class="list-group kanban-column"
            :list="arrDone"
            group="tasks"
          >
            <div
              class="list-group-item done"
              v-for="element in arrDone"
              :key="element.name"
            >
              {{ element.name }}
            </div>
          </draggable>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */

//import draggable
import draggable from "vuedraggable";
import Navbar from "./Navbar.vue";

export default {
  name: "Kanban",
  components: {
    draggable,
    Navbar,
  },
  data() {
    return {
      newTask: "",
      arrTasks: [
        { id: 1, name: "Design a Dashboard" },
        { id: 2, name: "Work on the task" },
        { id: 3, name: "complete the task" },
        { id: 4, name: "learn something new" },
      ],
      arrInProgress: [
        { id: 5, name: "Do the task" },
        { id: 6, name: "learn anything new" },
      ],
      arrDone: [],
    };
  },
  methods: {
    add: function () {
      if (this.newTask) {
        this.arrTasks.push({ name: this.newTask });
        this.newTask = "";
      }
    },
  },
};
</script>

<style scope>
.container {
  max-width: 80%;
  width: 100%;
  max-height: 100%;
  background-color: rgba(255, 255, 255, 0.3);
  padding: 25px;
  border-radius: 25px;
  overflow: auto;
  color: #222;
}
h3 {
  font-size: 22px;
  font-weight: bold;
}
.kanban-column {
  min-height: 300px;
  cursor: move;
}
.done {
  color: rgb(105, 145, 45);
  text-decoration: line-through;
}
</style>