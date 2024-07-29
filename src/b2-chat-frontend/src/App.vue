<script lang="ts">
import { ref } from 'vue';
import { b2_chat_backend } from '../../declarations/b2-chat-backend';

export default {
  data() {
    return {
      newNote: "",
      notes: [] as string[]
    }
  },
  methods: {
    async dodajNotatke() {
      await b2_chat_backend.add_note(this.newNote)
      await this.pobierzNotatki()
    },
    async pobierzNotatki() {
      this.notes = await b2_chat_backend.get_notes()
    }
  },
  mounted(){
    this.pobierzNotatki()
  }
}
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
      <div>
      {{ notes }}
    </div>
    <div>
      <textarea v-model="newNote"></textarea><button @click="dodajNotatke">Dodaj notatke</button>
    </div>
  </main>
</template>
