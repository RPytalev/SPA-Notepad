<template>
    <div class="tag">
        {{item}}
    </div>
</template>

<script>
    export default {
        name: 'Tag',
        props: {
            item: String
        }
    }
</script>

<style lang="sass" scoped>
.tag
    display: flex
    width: auto
    height: 1.5rem
    padding: .1rem 1rem
    margin: .2rem .1rem
    background-color: #000
    color: red
    border: .1rem solid #fff
</style>