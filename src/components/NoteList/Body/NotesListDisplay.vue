<template>
    <div class="notes-list-display">
        <DeleteNoteBtn @delete-note="deleteNote" />
        <div class="notes-list">
            <NotesList :selectedNoteId="selectedNoteId" 
                       :notesList="notesList" 
                       @note-selected="noteSelected" 
                       @switch-reminder="switchReminder" />
        </div>
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
        }
    }
</script>

<style lang="sass" scoped>
.notes-list-display,
.found-notes-list-display
    width: 20rem
    height: 20rem
    margin: 1rem
    background-color: pink
    color: magenta
</style>