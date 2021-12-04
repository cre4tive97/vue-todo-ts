<template>
  <li>
    <span @click="toggleItem" class="item"> {{ todoItem }}</span>
    <button @click="removeItem">삭제</button>
  </li>
</template>

<script lang="ts">
import { Todo } from "@/App.vue";
import Vue, { PropType } from "vue";

export default Vue.extend({
  props: {
    todoItem: {
      type: Object as PropType<Todo>,
      required: true,
    },
    todoIndex: {
      type: Number,
      required: true,
    },
  },
  methods: {
    toggleItem() {
      this.$emit("toggle", this.todoItem, this.todoIndex);
    },
    removeItem() {
      this.$emit("remove", this.todoIndex);
    },
  },
});
</script>

<style scoped>
.item {
  cursor: pointer;
}
.complete {
  text-decoration: line-through;
}
</style>
