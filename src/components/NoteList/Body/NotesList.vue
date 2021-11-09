<template>
    <div class="notes-list">
        <div :key="item.id" v-for="item in notesList">
            <NotesListItem 
            :selectedNoteId="selectedNoteId" 
            :item="item" 
            @click-select-note="sendSelectedNoteId" 
            @dblclick-switch-reminder="switchReminder" />
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
        methods: {
            sendSelectedNoteId(id) {
                this.$emit('click-select-note', id);
            },
            switchReminder(id) {
                this.$emit('dblclick-switch-reminder', id);
            }
        },
        props: {
            notesList: Array,
            selectedNoteId: Number
        }
    }
</script>

<style lang="sass" scoped>
::-webkit-scrollbar
  width: 0

.notes-list
    display: flex
    flex-flow: column
    width: 100%
    padding-left: 1rem
</style>