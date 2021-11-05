<template>
    <div class="notes-list-header">
        <button class="btn" @click="$emit('delete-note')">Delete Note</button>
    </div>
</template>

<script>
    export default {
        name: 'DeleteNoteBtn'
    }
</script>

<style lang="sass" scoped>
.notes-list-header
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