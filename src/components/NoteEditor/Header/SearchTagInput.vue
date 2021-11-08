<template>
    <div>
        <input type="text" v-on:mouseleave="tagInput">
    </div>
</template>

<script>
    export default {
        name: 'SearchTagInput',
        methods: {
            tagInput(event) {
                let searchTag = event.target.value;
                this.$emit('tag-input', searchTag);
            }
        }
    }
</script>

<style lang="sass" scoped>
input
    width: 8rem
    height: 1rem
    margin-right: .2rem
</style>