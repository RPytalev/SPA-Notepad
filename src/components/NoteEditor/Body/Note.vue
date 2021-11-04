<template>
    <div class="note-editor-display">
        <CreateNoteBtn @create-note="createNote" />
        <div>
            <div class="textarea">
                <NoteEdit :note="note" @edit-note="editNote" />
            </div>
            <div class="tags-list">
                <TagsList />
            </div>
            <div>
                <NoteView :note="note" />
            </div>
        </div>
    </div>
</template>

<script>
    import CreateNoteBtn from '../Header/CreateNoteBtn.vue'
    import NoteEdit from './NoteEdit.vue'
    import TagsList from '../../TagsList.vue'
    import NoteView from './NoteView.vue'

    export default {
        name: 'NoteEditorDisplay',
        components: {
            CreateNoteBtn,
            NoteEdit,
            TagsList,
            NoteView
        },
        methods: {
            createNote() {
                this.$emit('create-note');
            },
            editNote(noteChange) {
                this.$emit('edit-note', noteChange);
            }
        },
        props: {
            note: Object,
            showNewTextarea: Boolean,
        },
    }
</script>

<style lang="sass" scoped>
.note-editor-display 
    width: 20rem
    height: 20rem
    margin: 1rem
    background-color: pink
    color: magenta

    .tags-list
        width: 100%
        height: 4rem
        background-color: #000
</style>