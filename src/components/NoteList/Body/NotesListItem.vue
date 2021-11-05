<template>
    <div :class="[item.reminder ? 'reminder' : '', 'note', item.id == selectedNoteId ? 'selected' : 'note']" @click="$emit('note-selected', item.id)" @dblclick="$emit('switch-reminder', item.id)">
        <h3>{{ title }}</h3>
        <p>{{ item.date }}</p>
    </div>
</template>

<script>
    export default {
        name: 'NotesListItem',
        props: {
            item: Object,
            selectedNoteId: Number
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
    display: flex
    flex-flow: column
    width: 10rem
    height: 3rem
    margin-bottom: .1rem
    background-color: gray
    color: #fff
    -webkit-user-select: none 
    overflow: hidden
    cursor: pointer

.reminder
    border-left: .3rem solid #ff7800

.selected
    background-color: #000
</style>