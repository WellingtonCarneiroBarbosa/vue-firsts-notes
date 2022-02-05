<template>
    <div class="flex w-screen h-screen text-gray-700 m-2 mt-0">
      <div class="flex flex-col flex-grow">
        <ul class="mt-2" v-for="(comment, index) in allComments" :key="index">
          <li class="mb-2 mt-2">
            <p>Autor: {{ comment.author }}</p>
            <p>Nota: {{ comment.comment }}</p>
            <a href="#" class="mt-1 text-red-500 italic" v-on:click.prevent="deleteComment(index)">Delete</a>
          </li>

          <hr>
        </ul>

        <div class="flex flex-col flex-grow overflow-auto mt-4">
          <label class="mb-2 text-gray-700" for="comment">Type some comment...</label>
          <textarea 
            v-model="comment"
            v-on:keyup.enter="saveComment"
            id="comment"
            class="border border-gray-300 rounded focus:outline-none"
            />

            <button class="bg-gray-400 rounded p-2 mt-2" v-on:click="saveComment">Save Comment</button>
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
      comment: '',
      comments: []
    }
  },

  methods: {
    saveComment() {
      if(this.comment.trim() != '') {

        this.comments.push({
          comment: this.comment,
          author: ''
        });

        this.comment = ''
      }
    },

    deleteComment(id) {
      if(confirm('Are you sure you want to delete this comment?')) {
        this.comments.splice(id, 1);
      }
    }
  },

  computed: {
    allComments() {
      return this.comments.map(comment => ({
        ...comment,
        author: comment.author.trim() === '' ? 'Anônimo' : comment.author
      }));
    }
  },

  watch: {
    //
  }
}
</script>
