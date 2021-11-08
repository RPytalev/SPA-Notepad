<template>
    <div class="note" @click="switchComponent">
        <p class="date">{{ this.note.date }}</p>
        <p class="title">{{ title }}</p>
        <p v-html="text"></p>
    </div>
</template>

<script>
    export default {
        name: 'NoteView',
        props: {
            note: Object
        },
        methods: {
            switchComponent() {
                this.$emit('switch-component');
            }
        },
        computed: {
            title: function() {
                let title = '';
                let titleGroup = this.note.rawText.match(/(.*?)\n/);
                if(titleGroup === undefined || titleGroup === null)
                {
                    title = this.note.rawText;
                } else {
                    title = titleGroup[0];
                }

                return title;
            },
            text: function() {
                let textWithoutTitle = this.note.rawText.replace(this.title, '');
                this.note.tags.forEach(tag => {
                    textWithoutTitle = textWithoutTitle.replaceAll(tag, '<span class=\'highlight\'>$&</span>');
                });

                return textWithoutTitle;
            }
        }
    }
</script>

<style lang="sass" scoped>
.note
    display: flex
    flex-flow: column
    width: 100%
    height: 100%
    margin: 0
    padding: 0
    background-color: #547
    color: #fff
    text-align: left
    font-family: Montserrat
    font-size: .8rem
    overflow-x: hidden
    overflow-y: auto

    p
        margin: 0
        padding: 0
    
    .date
        font-size: .5rem

.tags
    display: flex
    width: 100%
    height: 2rem
    background-color: #777
    
</style>
