<template>
    <div class="list-display">
        <div class="notes-list-header">
            <DeleteNoteBtn @delete-note="deleteNote" />
        </div>
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
.list-display
    display: flex
    flex-flow: column
    flex: 100%

    ::-webkit-scrollbar
        width: 0px
        background: transparent

    .notes-list-header
        display: flex
        justify-content: flex-end
        align-items: center
        width: 100%
        height: 4vh
        padding: 1rem 0
        background-color: rgb(42, 39, 39)
        border-bottom: .1rem solid #000

    .notes-list
        width: 100%
        overflow-x: hidden
        overflow-y: scroll
        scroll-behavior: smooth
</style>