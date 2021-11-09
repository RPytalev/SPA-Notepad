<template>
    <div role="button" id="create-note-btn" class="btn" @click="createNote">
        <img alt="Paper sheet and pen icon image" src="../../../assets/button-create-gray.svg">
    </div>

</template>

<script>
    export default {
        name: 'CreateNoteBtn',
        methods: {
            createNote() {
                this.$emit('btn-click-create');
            }
        }
    }
</script>

<style lang="sass" scoped>
.btn
    display: flex
    justify-content: center
    align-items: center
    width: 2rem
    height: 2rem
    margin: 0 1rem
    border: .1rem solid rgb(42, 39, 39)
    border-radius: 50%
    cursor: pointer

    img
        width: 2rem
        height: 2rem
        object-fit: contain

.btn:hover
    border: .1rem solid lightgray
</style>