<template>
  <h1 style="margin-top: 30px">Список текстов</h1>

  <ul class="list">
    <li class="list-item" v-for="item in texts" :key="item.id">
      {{ item.author }} : {{ item.text }}
      <button @click="delite(item.id)">Удалить</button>
      <button @click="edit(item.id)">Редактировать</button>
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      item: "",
    };
  },
  methods: {
    delite(id: number) {
      this.$emit("delite", id);
    },
    edit(id: number) {
      this.$emit("edit", id);
    },
  },
  props: {
    texts: {
      type: Object,
    },
  },
  emits: {
    delite: (id: number) => Number.isInteger(id),
    edit: (id: number) => Number.isInteger(id),
  },
});
</script>
