<template>
    <div class="notesListHeader">
        <div class="btn" @click="deleteNote">deleteNote</div>
    </div>
</template>

<script>
    export default {
        name: 'DeleteNoteBtn',
        methods: {
            deleteNote() {
                this.$emit('delete-note');
            }
        }
    }
</script>

<style lang="sass" scoped>
.notesListHeader 
    display: flex
    justify-content: flex-end
    align-items: center
    width: 100%
    height: 4rem
    background-color: orange

    .btn
        width: 10rem
        height: 2rem
        background-color: red
        color: #fff
</style>