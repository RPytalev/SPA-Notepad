<template>
    <div class="note-editor-display">
        <div class="header">
            <CreateNoteBtn @create-note="$emit('create-note')" />
        </div>
        <div class="display">
            <div class="textarea" v-show="switchNoteEditorState">
                <NoteEdit :note="note" @edit-note="editNote" @toggle-component="$emit('toggle-component')" />
            </div>
            <div class="note-view" v-show="!switchNoteEditorState">
                <NoteView :note="note" @switch-component="$emit('switch-component')" />
            </div>
        </div>
        <div class="tags-list">
            <TagsList :note="note" />
        </div>
    </div>
</template>

<script>
    import CreateNoteBtn from '../Header/CreateNoteBtn.vue'
    import NoteEdit from './NoteEdit.vue'
    import NoteView from './NoteView.vue'
    import TagsList from '../../TagsList.vue'

    export default {
        name: 'NoteEditorDisplay',
        components: {
            CreateNoteBtn,
            NoteEdit,
            NoteView,
            TagsList
        },
        props: {
            note: Object,
            switchNoteEditorState: Boolean,
        },
        methods: {
            editNote(noteChange) {
                this.$emit('edit-note', noteChange)
            }
        },
        emits: ['switch-component', 'toggle-component', 'create-note']
    }
</script>

<style lang="sass" scoped>
.note-editor-display 
    display: flex
    flex-flow: column
    width: 20rem
    height: 20rem

    .header
        display: flex
        width: 100%
        height: 4rem
        background-color: #ff5800
    
    .display 
        display: flex
        position: relative
        width: 20rem
        height: 20rem

        .textarea
            display: flex
            position: absolute
            width: 100%
            height: 100%
            top: 0
            left: 0
            
        .note-view
            display: flex
            position: absolute
            width: 100%
            height: 100%
            top: 0
            left: 0

    .tags-list
        display: flex
        width: 100%
        height: 4rem
        background-color: #ff5800
</style>