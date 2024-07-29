<script lang="'ts'">
import { ref } from 'vue';
import { chat_backend } from '../../declarations/chat_backend';

export default{
  data(){
    return {
      newNote: "",
      notes: []
    }
  },
  methods: {
    async addNote(){
      await chat_backend.add_note(this.newNote)
      await this.getNotes()
    },
    async getNotes() {
      this.notes = await chat_backend.get_notes()
    }
  },
  mounted(){
    this.getNotes()
  }
}
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <div>
      {{ newNote }}
    </div>
    <div>
      <textarea v-model="newNote"></textarea
      ><button @click="addNote">Add Note</button>
    </div>
  </main>
</template>
