<template>
    <div>
        <input type="text" v-on:mouseleave="tagInput">
    </div>
</template>

<script>
    export default {
        name: 'TagInput',
        methods: {
            tagInput(event) {
                let inputTag = event.target.value;
                this.$emit('tag-input', inputTag, event);
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