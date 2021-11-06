<template>
    <div class="note-input-tag">
        <!-- <h3>{{ title }}</h3> -->
        <p class="date">{{ item.date }}</p>
        <p class="text">{{ item.rawText }}</p>
    </div>
</template>

<script>
    export default {
        name: 'NoteInputTag',
        props: {
            item: Object
        }
    }
</script>

<style lang="sass" scoped>
.note-input-tag
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
    p
        margin: 0
        padding: 0 
    
    .date
        font-size: .5rem
</style>