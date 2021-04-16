<template>
  <div class="container" style="margin-top: 20px">
    <div class="card">
      <div class="card-body">
        <h5 class="card-title">Simple Todo App</h5>
        <div class="row">
          <div class="col-10">
            <input
              v-model="todo"
              type="text"
              class="form-control"
              @keyup.enter="add"
            />
          </div>
          <div class="col-auto">
            <button class="btn btn-success" @click="add">Add</button>
          </div>
        </div>
        <list :todos="todos" @deleteTodo="deleteTodo" @doneTodo="doneTodo" />
        <small>Total Todo : {{ totalTODO }}</small>
      </div>
    </div>
  </div>
</template>

<script>
import List from "./components/List.vue";
export default {
  components: { List },
  data() {
    return {
      todo: "",
      todos: [],
    };
  },
  mounted() {
    this.todos = JSON.parse(localStorage.getItem('todos'));
  },
  computed: {
    totalTODO() {
      return this.todos.length;
    },
  },
  methods: {
    add() {
      this.todos.unshift({
        activity: this.todo,
        isDone: false,
      });
      this.todo = "";
      this.saveToLocalSTorage();
    },
    deleteTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index != todoIndex) {
          return item;
        }
      });
      this.saveToLocalSTorage();
    },
    doneTodo(todoIndex) {
      this.todos = this.todos.filter((item, index) => {
        if (index == todoIndex) {
          item.isDone = true;
        }

        return item;
      });
      this.saveToLocalSTorage();
    },
    saveToLocalSTorage() {
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
  },
};
</script>

<style>
</style>