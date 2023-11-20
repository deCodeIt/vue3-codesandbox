<!--
1. Todo List Item component -> checkbox + title
- checked: boolean
- title: string

2. TodoList component -> Array of TodoListItem


-->

<template>
  <div>
    <button @click="addTodo">Add</button>
    <input type="text" @keyup.enter="addTodo" v-model="newTodoTitle" />
    <TodoListItem
      v-for="todo in todos"
      :key="todo.id"
      :title="todo.title"
      :isChecked="todo.isChecked"
      @checkevent="(newVal) => updateTodoStatus(todo.id, newVal)"
      @deleteevent="() => deleteTodo(todo.id)"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import TodoListItem from "@/components/TodoListItem.vue";

interface ITodoItem {
  id: number;
  title: string;
  isChecked: string;
}

export default defineComponent({
  components: {
    TodoListItem,
  },
  data() {
    return {
      isAdding: false,
      newTodoTitle: "",
      latestId: 1,
      todos: [] as ITodoItem[],
    };
  },
  methods: {
    generateId() {
      return this.latestId++;
    },
    updateTodoStatus(id: number, newVal: boolean) {
      this.todos.find((todo) => todo.id === id).isChecked = newVal;
      console.log("updateTodo", this.todos);
    },
    deleteTodo(id: number) {
      const idx = this.todos.findIndex((todo) => todo.id === id);
      this.todos.splice(idx, 1);
      console.log("deleteTodo", this.todos);
    },
    addTodo() {
      console.log("addTodo");
      const id = this.generateId();
      this.todos.push({
        id,
        title: this.newTodoTitle,
        isChecked: false,
      });
      // Reset form
      this.newTodoTitle = "";
      this.isAdding = false;
      console.log("addTodo", this.todos);
    },
  },
});
</script>

<style scoped></style>
