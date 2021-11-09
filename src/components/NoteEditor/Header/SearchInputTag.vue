<template>
    <div>
        <input id="search-tag-input" type="text" v-on:mouseleave="sendInputTag">
    </div>
</template>

<script>
    export default {
        name: 'SearchInputTag',
        methods: {
            sendInputTag(event) {
                let searchTag = event.target.value;
                this.$emit('mouseleave-input-tag', searchTag, event);
            }
        }
    }
</script>

<style lang="sass" scoped>
#search-tag-input
    height: 2rem
    outline: none
    border: .1rem solid #4a4545
    border-radius: .2rem
    background-color: rgb(42, 39, 39)
    caret-color: #ff7800
    color: lightgrey

#search-tag-input:hover
    border: .1rem solid gray
</style>