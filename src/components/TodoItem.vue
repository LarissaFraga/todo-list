<template>
  <InputText v-model="description" />
  <div class="div-buttons">
    <Button @click="cancel">Back</Button>
    <Button @click="save">Save</Button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      description: "",
    };
  },
  props: {
    todo: Object,
  },
  created() {
    if (this.todo) {
      this.description = this.todo.description;
    }
  },
  methods: {
    cancel() {
      this.$emit("cancel");
    },
    save() {
      this.$emit("saveTodo", { ...this.todo, description: this.description });
    },
  },
};
</script>

<style scoped>
.div-buttons {
  margin-top: 1rem;
  display: flex;
  gap: 1rem;
}
</style>
