<template>
  <h1 style="margin-top: 30px">Список текстов</h1>

  <ul class="list">
    <li class="list-item" v-for="item in texts" :key="item.id">
      {{ item.text }}
    </li>
  </ul>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  methods: {},
  props: {
    texts: {
      type: Object,
    },
  },
});
</script>
