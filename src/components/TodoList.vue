<template>
  <div class="todo-list">
    <div v-for="(todo, index) in todos" :key="index" class="todo-item">
      <label class="todo-label">{{ todo.description }}</label>
      <Button
        icon="pi pi-pencil"
        class="p-button-rounded p-button-text"
        @click="$emit('editTodo', index)"
      />
      <Button
        icon="pi pi-trash"
        class="p-button-rounded p-button-text"
        @click="$emit('deleteTodo', index)"
      />
    </div>
  </div>
</template>

<script>
export default {
  props: {
    todos: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.todo-list {
  margin-top: 1rem;
}
.todo-item {
  display: flex;
  align-items: center;
  border-bottom: 1px solid lightgray;
}
.todo-label {
  flex: 1;
}
</style>
