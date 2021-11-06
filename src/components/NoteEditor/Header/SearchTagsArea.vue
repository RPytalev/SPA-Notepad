<template>
    <div class="search-area">
        <TagInput @tag-input="tagInput" />
        <SearchTagButton @click="searchTag" />
    </div>
</template>

<script>
import SearchTagButton from './SearchTagButton.vue'
import TagInput from './TagInput.vue'

    export default {
        name: 'SearchTagsArea',
        components: {
            SearchTagButton,
            TagInput
        },
        methods: {
            tagInput(inputTag, event) {
                this.$emit('tag-input', inputTag, event);
            },
            searchTag() {
                this.$emit('search-tag');
            }
        }
    }
</script>

<style lang="sass" scoped>
.search-area
    display: flex
    width: 14rem
    height: 2rem
    background-color: red
</style>