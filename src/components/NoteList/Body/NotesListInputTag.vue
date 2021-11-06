<template>
    <div class="notes-list-input-tag" >
        <div >
            <NoteInputTag 
            :item="item" 
            :key="item.id" 
            v-for="item in notesListSelectedTag" />
        </div>
    </div>
</template>

<script>
import NoteInputTag from './NoteInputTag.vue'
    export default {
        name: 'NotesListInputTag',
        components: {
            NoteInputTag
        },
        props: {
            notesListSelectedTag: Array
        }
    }
</script>

<style lang="sass" scoped>
::-webkit-scrollbar
  width: 0

.notes-list-input-tag
    display: flex
    flex-flow: column
    width: 10rem
    height: 10rem
    background-color: #000
    color: magenta
    overflow-y: scroll
</style>