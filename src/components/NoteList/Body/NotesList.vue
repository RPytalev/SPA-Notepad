<template>
    <div class="notes-list">
        <div :key="item.id" v-for="item in notesList">
            <NotesListItem :selectedNoteId="selectedNoteId" :item="item" @note-selected="$emit('note-selected', item.id)" @switch-reminder="$emit('switch-reminder', item.id)" />
        </div>  
    </div>  
</template>

<script>
import NotesListItem from './NotesListItem.vue'
    export default {
        name: 'NotesList',
        components: {
            NotesListItem
        },
        props: {
            notesList: Array,
            selectedNoteId: Number
        },
        emits: ['note-selected', 'switch-reminder']
    }
</script>

<style lang="sass" scoped>
::-webkit-scrollbar
  width: 0

.notes-list
    display: flex
    flex-flow: column
    width: 10rem
    height: 10rem
    background-color: #000
    color: magenta
    overflow-y: scroll
</style>