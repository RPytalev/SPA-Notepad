<template>
    <div class="new-note">
         <textarea id="new-textarea" name="new-textarea" @change="createNewNote" v-model="text"></textarea>
    </div>
</template>

<script>
    export default {
        name: 'NewNoteTextarea',
        data() {
            return {
                id: '',
                text: '',
                date: '',
                reminder: false
            }
        },
        methods: {
            createNewNote() {

                let currentDate = new Date();

                const newNote = {
                    id: Math.floor(Math.random() * 1000),
                    text: this.text,
                    date: currentDate,
                    reminder: this.reminder
                }

                const newTags = document.querySelector('#new-textarea').value.match(/#[a-z A-Z 0-9]+/g);
                console.log(newTags);
                this.$emit('create-new-note', newNote, newTags);

                this.id = '';
                this.text = '';
                this.date = '';
                this.reminder = false;
            }
        }
    }
</script>

<style lang="sass" scoped>
.new-note
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