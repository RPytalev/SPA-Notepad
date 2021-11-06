<template>
    <div class="btn">
        <button @click="createNote">New Note</button>
    </div>
</template>

<script>
    export default {
        name: 'CreateNoteBtn',
        methods: {
            createNote() {
                this.$emit('create-note');
            }
        }
    }
</script>

<style lang="sass" scoped>
.btn 
    display: flex
    justify-content: flex-start
    align-items: center
    width: 100%
    height: 2rem
    background-color: orange

    button
        width: 5rem
        height: 2rem
        margin: 0 .2rem
        background-color: green
</style>