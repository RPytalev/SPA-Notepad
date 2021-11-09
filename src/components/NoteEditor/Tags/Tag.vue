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
    justify-content: center
    align-items: center
    width: auto
    height: 2rem
    padding: .2rem 1rem
    margin: .2rem
    background-color: #ff7800
    color: #fff
</style>