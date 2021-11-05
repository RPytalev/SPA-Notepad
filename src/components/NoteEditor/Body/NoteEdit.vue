<template>
    <div class="note-edit" v-on:mouseleave="$emit('toggle-component')">
        <div class="date">{{ note.date }}</div>
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
    width: 100%
    height: 100%

    .date
        background-color: #222
        color: #fff
        font-size: .5rem
        text-align: left

    textarea
        margin: 0
        padding: 0
        width: 100%
        height: 100%
        border: none
        background-color: #222
        color: #fff
        font-family: Montserrat
        font-size: .8rem
        resize: none
        outline: none
        overflow: auto
</style>