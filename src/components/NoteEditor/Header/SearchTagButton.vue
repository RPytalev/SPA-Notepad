<template>
    <div role="button" id="search-tag-btn" class="btn" @click="changeSearchTag">
        <img alt="Magnifier icon image" src="../../../assets/button-search-gray.svg">
    </div>
</template>

<script>
    export default {
        name: 'SearchTagButton',
        methods: {
            changeSearchTag() {
                this.$emit('change-search-tag');
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
    border: .1rem solid rgb(42, 39, 39)
    border-radius: 50%
    margin: 0 1rem
    cursor: pointer

    img
        width: 2rem
        height: 2rem
        object-fit: contain
    
.btn:hover
    border: .1rem solid lightgray
</style>