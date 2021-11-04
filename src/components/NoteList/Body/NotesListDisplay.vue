<template>
    <div class="notesListDisplay">
        <DeleteNoteBtn @delete-note="deleteNote" />
        <NotesList :selectedNoteId="selectedNoteId" :notesList="notesList" @note-selected="noteSelected" @switch-reminder="switchReminder" />
    </div>
</template>

<script>
import DeleteNoteBtn from '../Header/DeleteNoteBtn.vue'
import NotesList from './NotesList.vue'
    export default {
        name: 'NotesListDisplay',
        components: {
            DeleteNoteBtn,
            NotesList
        },
        props: {
            notesList: Array,
            deleteNoteId: Number,
            selectedNoteId: Number
        },
        methods: {
            switchReminder(id) {
                this.$emit('switch-reminder', id);
            },
            deleteNote() {
                this.$emit('delete-note');
            },
            noteSelected(id) {
                this.$emit('note-selected', id);
            }
        },
        emits: ['switch-reminder', 'delete-note', 'note-selected']
    }
</script>

<style lang="sass" scoped>
.notesListDisplay
    width: 20rem
    height: 20rem
    margin: 1rem
    background-color: pink
    color: magenta
</style>