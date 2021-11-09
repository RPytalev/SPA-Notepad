<template>
    <div class="list-display">
        <div class="notes-list-header">
            <DeleteNoteBtn @btn-click-delete="deleteNote" />
        </div>
        <div class="notes-list-body">
            <NotesList :selectedNoteId="selectedNoteId" 
                       :notesList="notesList" 
                       @click-select-note="sendSelectedNoteId" 
                       @dblclick-switch-reminder="switchReminder" />
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
                this.$emit('dblclick-switch-reminder', id);
            },
            deleteNote() {
                this.$emit('btn-click-delete');
            },
            sendSelectedNoteId(id) {
                this.$emit('click-select-note', id);
            }
        }
    }
</script>

<style lang="sass" scoped>
.list-display
    display: flex
    flex-flow: column
    width: 100%

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

    .notes-list-body
        display: flex
        width: 100%
        overflow-x: hidden
        overflow-y: scroll
        scroll-behavior: smooth
</style>