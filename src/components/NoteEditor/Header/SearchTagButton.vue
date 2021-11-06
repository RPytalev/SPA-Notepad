<template>
    <div class="search-tag-button">
        <button @click="searchTag">Search</button>
    </div>
</template>

<script>
    export default {
        name: 'SearchTagButton',
        methods: {
            searchTag() {
                this.$emit('search-tag');
            }
        }
    }
</script>

<style lang="sass" scoped>
button
    display: flex
    width: 4rem
    height: 1.4rem
</style>