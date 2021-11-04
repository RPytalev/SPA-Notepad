<template>
    <div class="notes-editor-header">
        <button @click="$emit('create-note')">New Note</button>
    </div>
</template>

<script>
    export default {
        name: 'CreateNoteBtn'
    }
</script>

<style lang="sass" scoped>
.notes-editor-header 
    display: flex
    justify-content: flex-start
    align-items: center
    width: 100%
    height: 4rem
    background-color: orange

    button
        width: 10rem
        height: 2rem
        background-color: green
</style>