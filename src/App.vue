<template>
  <h2>Todo App</h2>
  <div v-if="!editMode">
    <Button @click="newTodo">New</Button>
    <todo-list :todos="todos" @deleteTodo="deleteTodo" @editTodo="editTodo" />
  </div>
  <todo-item
    v-if="editMode"
    @cancel="cacel"
    @saveTodo="saveTodo"
    :todo="todo"
  />
</template>

<script>
import TodoItem from "./components/TodoItem.vue";
import TodoList from "./components/TodoList.vue";

export default {
  components: {
    TodoItem,
    TodoList,
  },

  data() {
    return {
      editMode: false,
      todos: [],
      todo: null,
      nextId: 1,
    };
  },
  methods: {
    newTodo() {
      this.editMode = true;
    },
    cacel() {
      this.editMode = false;
    },
    saveTodo(todo) {
      if (todo.id) {
        //edit
        const index = this.todos.findIndex((item) => item.id === todo.id);
        this.todos[index] = todo;
      } else {
        //add
        todo = { id: this.nextId, ...todo };
        this.todos.push(todo);

        this.nextId++;
        localStorage.setItem("nextId", this.nextId);
      }

      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.editMode = false;
    },
    deleteTodo(index) {
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos));
    },
    editTodo(index) {
      this.todo = this.todos[index];
      this.editMode = true;
    },
  },
  created() {
    const todos = localStorage.getItem("todos");
    if (todos) {
      this.todos = JSON.parse(todos);
    }

    const nextId = localStorage.getItem("nextId");
    if (nextId) {
      this.nextId = parseInt(nextId);
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: #2c3e50;
}
</style>
