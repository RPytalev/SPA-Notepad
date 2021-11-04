<template>
    <div class="note-edit">
        <textarea id="textarea" name="textarea" :value="note.rawText" @change="editNote"></textarea>
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
            }
        },
        props: {
            note: Object
        },
    }
</script>

<style lang="sass" scoped>
.note-edit
    width: 10rem
    height: 10rem
    margin: 1rem

    .title
        width: 100%
        height: 2rem
        background-color: #000
        margin: .2rem
        color: #fff

    textarea
        width: 100%
        height: 100%
        border: none
        background-color: #000
        color: #fff
</style>