<template>
    <div class="tag">
        <div v-if="tagDisplayState">
            {{ tag }}
        </div>
    </div>
</template>

<script>
    export default {
        name: 'Tag',
        props: {
            tag: String,
            tagDisplayState: Boolean
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
    color: #fff
    border: .1rem solid #fff
</style>