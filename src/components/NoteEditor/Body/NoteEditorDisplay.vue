<template>
    <div class="editor-display">
        <div class="note-editor-header">
            <div class="button">
                <CreateNoteBtn @btn-click-create="createNote" />
            </div>
            <div class="search-area">
                <SearchTagsArea 
                @btn-click-search="searchNote" />
            </div>
        </div>
        <div class="display">
            <div class="note-edit" v-show="switchNoteEditorState">
                <NoteEdit 
                :note="note" 
                @textarea-change-edit="editNote"
                @mouseleave-note-editor="toggleNoteEditor" />
            </div>
            <div class="note-view" v-show="!switchNoteEditorState">
                <NoteView 
                :note="note"
                @btn-click-toggle-display="toggleNoteDisplay" />
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
                this.$emit('btn-click-create');
            },
            editNote(noteChange) {
                this.$emit('textarea-change-edit', noteChange)
            },
            searchNote(searchTag) {
                this.$emit('btn-click-search', searchTag);
            },
            toggleNoteEditor() {
                this.$emit('mouseleave-note-editor');
            },
            toggleNoteDisplay() {
                this.$emit('btn-click-toggle-display');
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