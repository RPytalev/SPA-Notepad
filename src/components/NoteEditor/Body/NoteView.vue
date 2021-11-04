<template>
    <div>
        <div>Title : {{ title }}</div>
        <div>Date : {{ note.date }}</div>
        <div>Text : {{ text }}</div>
    </div>
</template>

<script>
    export default {
        name: 'NoteView',
        props: {
            note: Object
        },
        computed: {
            title: function () {
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
            text: function () {
                let textWithoutTitle = this.note.rawText.replace(this.title, '');
                return textWithoutTitle;
            }
        }
    }
</script>

<style lang="sass" scoped>

</style>
