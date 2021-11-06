<template>
    <div class="notes-list-display">
        <DeleteNoteBtn @delete-note="deleteNote" />
        <div class="notes-list" v-show="switchLists">
            <NotesList :selectedNoteId="selectedNoteId" :notesList="notesList" @note-selected="noteSelected" @switch-reminder="switchReminder" />
        </div>
        <div class="notes-list-input-tag" v-show="!switchLists">
            <NotesListInputTag
            :notesListSelectedTag="notesListSelectedTag" />
        </div>
    </div>
</template>

<script>
import DeleteNoteBtn from '../Header/DeleteNoteBtn.vue'
import NotesList from './NotesList.vue'
import NotesListInputTag from './NotesListInputTag.vue'
    export default {
        name: 'NotesListDisplay',
        components: {
            DeleteNoteBtn,
            NotesList,
            NotesListInputTag
        },
        props: {
            notesList: Array,
            deleteNoteId: Number,
            selectedNoteId: Number,
            switchLists: Boolean,
            notesListSelectedTag: Array
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
.notes-list-display
    width: 20rem
    height: 20rem
    margin: 1rem
    background-color: pink
    color: magenta
</style>