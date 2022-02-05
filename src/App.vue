<template>
    <div class="flex w-screen h-screen text-gray-700">
      <div class="flex flex-col flex-shrink-0 w-64 border-r border-gray-300 bg-gray-100">
        <!-- sidebar -->
        <ul v-for="(note, index) in allNotes" :key="index">
          <li>
            <p>{{ note.note }}</p>
          </li>
        </ul>

      </div>

      <div class="flex flex-col flex-grow">
        <!-- Content -->
        <div class="flex flex-col flex-grow overflow-auto m-2">
          <label class="mb-2 text-gray-700" for="note">Type some note...</label>
          <textarea 
            v-model="note"
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

  data: function () {
    return {
      note: '',
      notes: []
    }
  },

  methods: {
    saveNote() {
      if(this.note.trim() != '') {

        if(confirm('Are you sure you want to save this note?')) {
          this.notes.push({
            note: this.note
          });

          this.note = ''
        }
      }
    }
  },

  computed: {
    allNotes() {
      let notes = this.notes;

      // check empty array
      if(notes.length === 0) {
        return [{
          note: 'Add some note your son of a bitch'
        }];
      }

      return notes;
    }
  }


}
</script>
