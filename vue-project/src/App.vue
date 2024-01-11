<script setup lang="ts">
import HelloWorld from "./components/Input.vue";
import Texts from "./components/Texts.vue";
</script>

<template>
  <input
    class="mainInput"
    type="text"
    placeholder="Напишите ваш текст"
    @keyup.enter="addText"
    v-model="writeText"
  />

  <Texts :texts="texts" />
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      texts: [
        {
          id: 1,
          text: "Элемент 1 Lorem ipsum, dolor sit amet consectetur adipisicing elit. Sapiente unde, delectus est voluptas ducimus architecto laborum. Deserunt et eligendi consequuntur, quasi labore cupiditate, id enim veritatis aperiam, quo eos aspernatur.",
        },
        { id: 2, text: "Элемент 2" },
        { id: 3, text: "Элемент 3" },
      ],

      writeText: "",
    };
  },

  methods: {
    addText() {
      console.log("Клик на Enter");
      this.texts.push({ id: Date.now(), text: this.writeText });
    },
  },
});
</script>
