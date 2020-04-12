<template>
  <div>
    <form
      class="bg-blue-100 border border-blue-200 flex flex-col max-w-sm mx-auto p-6 rounded"
      @submit.prevent="createNewNote"
    >
      <label for="note-title">
        Título
      </label>
      <input
        class="border border-gray-400 outline-none px-3 py-2 rounded"
        id="note-title"
        type="text"
        v-model="title"
      />
      <label for="note-content">
        Contenido
      </label>
      <textarea
        class="border border-gray-400 outline-none px-3 py-2 rounded"
        id="note-content"
        type="text"
        v-model="content"
      ></textarea>
      <button
        class="bg-green-500 border border-green-600 mt-4 outline-none py-2 px-3 rounded text-white"
        type="submit"
      >
        Crear nota
      </button>
    </form>
    <div
      class="bg-green-300 border border-green-400 max-w-sm mx-auto mt-4 py-2 px-3"
      v-if="showAlert"
    >
      Nota guardada correctamente
    </div>
  </div>
</template>

<script>
import uuid from "uuid/v4";
import { mapMutations } from "vuex";

export default {
  data: () => ({
    title: "",
    content: "",
    showAlert: false
  }),
  methods: {
    ...mapMutations(["addNewNote"]),
    createNewNote() {
      this.addNewNote({
        id: uuid(),
        title: this.title,
        content: this.content
      });

      this.showAlert = true;

      this.title = "";
      this.content = "";

      setTimeout(() => (this.showAlert = false), 1000);
    }
  }
};
</script>
