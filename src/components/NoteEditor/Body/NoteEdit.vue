<template>
    <div class="note-editor" v-on:mouseleave="toggleComponent">
        <p class="date">{{ this.note.date }}</p>
        <textarea id="textarea" name="textarea" 
        :value="this.note.rawText" 
        @change="editNote">
        </textarea>
    </div>
</template>

<script>
    export default {
        name: 'NoteEdit',
        methods: {
            editNote(event) {
                
                let rawText = event.target.value;
                
                const noteChange = {
                    id: this.note.id,
                    rawText: rawText,
                    date: new Date()
                }
                this.$emit('edit-note', noteChange);
            },
            toggleComponent() {
                this.$emit('toggle-component');
            }
        },
        props: {
            note: Object
        },
    }
</script>

<style lang="sass" scoped>
.note-editor
    display: flex
    flex-flow: column
    width: 100%
    background-color: rgb(42, 39, 39)
    margin: 0
    padding: 0
    color: #fff
    text-align: left

    p
        margin: 0
        padding: 0 1rem

    .date
        font-size: 1rem
        color: #fff

    textarea
        outline: none
        border: none
        resize: none
        width: 100%
        height: 100%
        background-color: rgb(42, 39, 39)
        caret-color: #ff7800
        color: #fff
        font-family: Montserrat
        font-size: 1.4rem
        font-weight: 300
        overflow: auto
        text-align: left
        padding: 0 1rem
        margin: 0
</style>