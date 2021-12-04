<template>
  <li>
    <span> {{ todoItem }}</span>
    <button @click="removeItem">삭제</button>
  </li>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  props: {
    todoItem: {
      type: String,
      required: true,
    },
    todoIndex: {
      type: Number,
      required: true,
    },
  },
  methods: {
    removeItem() {
      this.$emit("remove", this.todoIndex);
    },
  },
});
</script>

<style scoped></style>
