<script setup lang="ts">
import HelloWorld from "./components/Input.vue";
import Texts from "./components/Texts.vue";
</script>

<template>
  <input
    type="text"
    placeholder="Введите ваше имя"
    v-model="nextName"
    @keyup.enter="createName"
  />
  <p>{{ Name }}</p>
  <input
    v-if="edits.editMode == false"
    class="mainInput"
    type="text"
    placeholder="Напишите ваш текст"
    @keyup.enter="addText"
    v-model="writeText"
  />

  <!-- Поле для редактирования текста -->
  <input
    v-if="edits.editMode == true"
    class="mainInput"
    type="text"
    v-model="edits.editText"
    @keyup.enter="createEdit"
  />

  <Texts :texts="texts" @delite="delite" @edit="edit" />
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  data() {
    return {
      texts: [
        {
          id: 1,
          author: "User",
          text: "Элемент 1 Lorem ipsum, dolor sit amet consectetur adipisicing elit. Sapiente unde, delectus est voluptas ducimus architecto laborum. Deserunt et eligendi consequuntur, quasi labore cupiditate, id enim veritatis aperiam, quo eos aspernatur.",
        },
        { id: 2, text: "Элемент 2", author: "User" },
        { id: 3, text: "Элемент 3", author: "User" },
      ],

      writeText: "",
      Name: "User",
      nextName: "",
      edits: {
        editMode: false,
        editText: "",
        editId: 0,
      },
    };
  },

  methods: {
    addText() {
      if (this.writeText) {
        this.texts.push({
          id: Date.now(),
          text: this.writeText,
          author: this.Name,
        });
        this.writeText = "";
      }
    },
    delite(id: number) {
      this.texts = this.texts.filter((item) => item.id != id);
    },
    edit(id: number) {
      this.edits.editMode = true;
      for (const text of this.texts) {
        if (text.id == id) {
          this.edits.editId = id;
          this.edits.editText = text.text;
        }
      }
    },
    createEdit() {
      this.texts.forEach((text) => {
        if (text.id == this.edits.editId) {
          text.text = this.edits.editText;
          this.edits.editText = "";
          this.edits.editId = 0;
          this.edits.editMode = false;
        }
      });
    },
    createName() {
      this.Name = this.nextName;
      this.nextName = "";
    },
  },
});
</script>
