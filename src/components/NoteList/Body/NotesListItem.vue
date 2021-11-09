<template>
    <div :class="[this.item.reminder ? 'reminder' : '', 'note', 
         this.item.id == selectedNoteId ? 'selected' : '']" 
         @click="noteSelected" 
         @dblclick="switchReminder">

        <h3>{{ title }}</h3>
        <p>{{ this.item.date }}</p>
        <hr size="1" color="#4a4545" />
    </div>
</template>

<script>
    export default {
        name: 'NotesListItem',
        props: {
            item: Object,
            selectedNoteId: Number
        },
        methods: {
            noteSelected() {
                this.$emit('note-selected', this.item.id);
            },
            switchReminder() {
                this.$emit('switch-reminder', this.item.id);
            }
        },
        computed: {
            title: function () {
                let title = '';
                let titleGroup = this.item.rawText.match(/(.*?)\n/);
                if(titleGroup === undefined || titleGroup === null)
                {
                    title = this.item.rawText;
                } else {
                    title = titleGroup[0];
                }
                return title;
            }
        }
    }
</script>

<style lang="sass" scoped>
.note
    width: 100%
    height: 8rem
    background-color: rgb(42, 39, 39)
    color: #fff
    cursor: pointer

hr
    position: relative
    display: flex
    justify-self: center
    width: 90%

.reminder
    border-left: .3rem solid aqua

.selected
    background-color: #ff7800
    user-select: none
</style>