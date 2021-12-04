<template>
  <div>
    <header>
      <h1>Vue Todo with Typescript</h1>
    </header>
    <main>
      <TodoInput
        :item="todoText"
        @input="updateTodoText"
        @add="addTodoItem"
      ></TodoInput>
    </main>
    <div>
      <ul>
        <TodoListItem
          v-for="(todoItem, i) in todoItems"
          :key="i"
          :todoItem="todoItem"
          :todoIndex="i"
          @remove="removeTodoItem"
        ></TodoListItem>
      </ul>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import TodoInput from "./components/TodoInput.vue";
import TodoListItem from "./components/TodoListItem.vue";

const STORAGE_KEY = "vue-todo-ts-v1";
const storage = {
  fetch() {
    const todoItems = localStorage.getItem(STORAGE_KEY) || "[]";
    const result = JSON.parse(todoItems);
    return result;
  },
  save(todoItems: any[]) {
    const parsed = JSON.stringify(todoItems);
    localStorage.setItem(STORAGE_KEY, parsed);
  },
};

export interface Todo {
  title: string;
  done: boolean;
}

export default Vue.extend({
  components: {
    TodoInput,
    TodoListItem,
  },
  data() {
    return {
      todoText: "",
      todoItems: [] as Todo[],
    };
  },
  created() {
    this.fetchTodoItems();
  },
  methods: {
    updateTodoText(currentValue: string) {
      this.todoText = currentValue;
    },
    addTodoItem() {
      const value = this.todoText;
      const todo: Todo = {
        title: value,
        done: false,
      };
      this.todoItems.push(todo);
      storage.save(this.todoItems);
      this.initTodoText();
    },
    initTodoText() {
      this.todoText = "";
    },
    fetchTodoItems() {
      this.todoItems = storage.fetch();
    },
    removeTodoItem(index: number) {
      console.log("remove", index);
      this.todoItems.splice(index, 1);
      storage.save(this.todoItems);
    },
  },
});
</script>

<style scoped></style>
