<template>
    <div class="flex w-screen h-screen text-gray-700">
      <div class="flex flex-col flex-shrink-0 w-4/12 border-r border-gray-300 bg-gray-100">
        <!-- sidebar -->
        <ul class="ml-2" v-for="(note, index) in allNotes" :key="index">
          <li class="mb-2 mt-2">
            <p>Autor: {{ note.author }}</p>
            <p>Nota: {{ note.note }}</p>
            <a href="#" class="mt-1 italic" v-on:click.prevent="deleteNote(index)">Delete</a>
          </li>

          <hr>
        </ul>

      </div>

      <div class="flex flex-col flex-grow">
        <!-- Content -->
        <div class="flex flex-col flex-grow overflow-auto m-2">
          <label class="mb-2 text-gray-700" for="note">Type some note...</label>
          <textarea 
            v-model="note"
            v-on:keyup.enter="saveNote"
            id="note"
            class="border border-gray-300 rounded focus:outline-none"
            />

            <button class="bg-gray-400 rounded p-2 mt-2" v-on:click="saveNote">Salvar Nota</button>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  components: {
    //
  },

  data() {
    return {
      note: '',
      notes: []
    }
  },

  methods: {
    saveNote() {
      if(this.note.trim() != '') {

        this.notes.push({
          note: this.note,
          author: ''
        });

        this.note = ''
      }
    },

    deleteNote(id) {
      if(confirm('Are you sure you want to delete this note?')) {
        this.notes.splice(id, 1);
      }
    }
  },

  computed: {
    allNotes() {
      return this.notes.map(note => ({
        ...note,
        author: note.author.trim() === '' ? 'Anônimo' : note.author
      }));
    }
  },

  watch: {
    //
  }
}
</script>
