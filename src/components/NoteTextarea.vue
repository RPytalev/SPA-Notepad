<template>
    <div class="note-textarea">
        <textarea id="textarea" name="textarea" @change="createNote" :value="note.text"></textarea>
    </div>
</template>

<script>
    export default {
        name: 'NoteTextarea',
        data() {
            return {
                id: '',
                text: '',
                date: '',
                reminder: false
            }
        },
        methods: {
            createNote() {

                let currentDate = new Date();

                const noteNew = {
                    id: Math.floor(Math.random() * 1000),
                    text: document.querySelector('textarea').value,
                    date: currentDate,
                    reminder: this.reminder
                }
                const tagsNew = document.querySelector('#textarea').value.match(/#[a-z A-Z 0-9]+/g);

                this.$emit('create-note', noteNew, tagsNew);

                this.id = '';
                this.text = '';
                this.date = '';
                this.reminder = false;
            }
        },
        props: {
            note: Object
        }
    }
</script>

<style lang="sass" scoped>
.note-textarea
    width: 10rem
    height: 10rem
    margin: 1rem

    textarea
        width: 100%
        height: 100%
        border: none
        background-color: #000
        color: #fff
</style>