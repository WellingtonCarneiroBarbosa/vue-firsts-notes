<template>
    <editor-content :editor="editor" />
</template>

<script>
import { Editor, EditorContent } from '@tiptap/vue-3'
import StarterKit from '@tiptap/starter-kit'

export default {
    name: 'TipTap',

    components: {
        EditorContent
    },

    data() {
        return {
            editor: null,
        }
    },

    mounted() {
        this.editor = new Editor({
        content: '<h3>Type something...</h3>',
        extensions: [
            StarterKit,
        ],
        editorProps: {
            attributes: {
            class: "prose my-6 mx-auto focus:outline-none"
            }
        }
        })
    },

    beforeUnmount() {
        this.editor.destroy()
    },
}
</script>