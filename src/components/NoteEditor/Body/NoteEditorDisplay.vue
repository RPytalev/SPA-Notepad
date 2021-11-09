<template>
    <div class="editor-display">
        <div class="note-editor-header">
            <div class="button">
                <CreateNoteBtn @create-note="createNote" />
            </div>
            <div class="search-area">
                <SearchTagsArea 
                @change-search-tag="changeSearchTag" />
            </div>
        </div>
        <div class="display">
            <div class="note-edit" v-show="switchNoteEditorState">
                <NoteEdit 
                :note="note" 
                @edit-note="editNote"
                @toggle-component="toggleComponent" />
            </div>
            <div class="note-view" v-show="!switchNoteEditorState">
                <NoteView 
                :note="note"
                @switch-component="switchComponent" />
            </div>
        </div>
        <div class="tags-list">
            <TagsList 
            :note="note"
            :tagDisplayState="tagDisplayState" />
        </div>
    </div>
</template>

<script>
    import CreateNoteBtn from '../Header/CreateNoteBtn.vue'
    import SearchTagsArea from '../Header/SearchTagsArea.vue'
    import NoteEdit from './NoteEdit.vue'
    import NoteView from './NoteView.vue'
    import TagsList from '../Tags/TagsList.vue'

    export default {
        name: 'NoteEditorDisplay',
        components: {
            CreateNoteBtn,
            SearchTagsArea,
            NoteEdit,
            NoteView,
            TagsList
        },
        props: {
            note: Object,
            switchNoteEditorState: Boolean,
            tagDisplayState: Boolean,
        },
        methods: {
            createNote() {
                this.$emit('create-note');
            },
            editNote(noteChange) {
                this.$emit('edit-note', noteChange)
            },
            changeSearchTag(searchTag) {
                this.$emit('change-search-tag', searchTag);
            },
            toggleComponent() {
                this.$emit('toggle-component');
            },
            switchComponent() {
                this.$emit('switch-component');
            }
        }
    }
</script>

<style lang="sass" scoped>
.editor-display
    display: flex
    flex-flow: column
    flex: 100%

    ::-webkit-scrollbar
        width: 0px
        background: transparent

    .note-editor-header
        display: flex
        justify-content: space-between
        align-items: center
        width: 100%
        height: 4vh
        padding: 1rem 0
        background-color: rgb(42, 39, 39)
        border-bottom: .1rem solid #000

    .display
        position: relative
        display: flex
        width: 100%
        flex: 95%
        background-color: rgb(42, 39, 39)

        .note-edit
            position: absolute
            display: flex
            left: 0
            top: 0
            width: 100%
            height: 100%

        .note-view
            position: absolute
            display: flex
            left: 0
            top: 0
            width: 100%
            height: 100%

    .tags-list
        display: flex
        align-items: center
        width: 100%
        flex: 5%
        background-color: rgb(42, 39, 39)
        border-top: .1rem solid #000
</style>