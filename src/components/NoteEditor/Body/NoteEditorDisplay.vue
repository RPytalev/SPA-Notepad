<template>
    <div class="note-editor-display">
        <div class="header">
            <div class="button">
                <CreateNoteBtn @create-note="createNote" />
            </div>
            <div class="search-area">
                <SearchTagsArea 
                @change-search-tag="changeSearchTag" 
                @tag-input="tagInput" />
            </div>
        </div>
        <div class="display">
            <div class="textarea" v-show="switchNoteEditorState">
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
.note-editor-display 
    display: flex
    flex-flow: column
    width: 20rem
    height: 20rem
    margin: 1rem

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