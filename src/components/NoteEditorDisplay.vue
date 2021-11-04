<template>
    <div class="note-editor-display">
        <CreateNewTextareaBtn @create-new-textarea="createNewTextarea" />
        <div>
            <div class="textarea" v-show="!showNewTextarea">
                <NoteTextarea :note="note" @create-note="createNote" />
            </div>
            <div class="new-textarea" v-show="showNewTextarea">
                <NewNoteTextarea :note="note" @create-new-note="createNewNote" />
            </div>
            <div class="tags-list">
                <TagsList :tagsList="tagsList" />
            </div>
        </div>
    </div>
</template>

<script>
    import CreateNewTextareaBtn from './CreateNewTextareaBtn.vue'
    import NoteTextarea from './NoteTextarea.vue'
    import NewNoteTextarea from './NewNoteTextarea.vue'
    import TagsList from './TagsList.vue'

    export default {
        name: 'NoteEditorDisplay',
        components: {
            CreateNewTextareaBtn,
            NoteTextarea,
            NewNoteTextarea,
            TagsList
        },
        methods: {
            createNote(noteNew, tagsNew) {
                this.$emit('create-note', noteNew, tagsNew);
            },
            createNewTextarea() {
                this.$emit('create-new-textarea');
            },
            createNewNote(newNote, newTags) {
                this.$emit('create-new-note', newNote, newTags);
            }
        },
        props: {
            note: Object,
            showNewTextarea: Boolean,
            tagsList: Array
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