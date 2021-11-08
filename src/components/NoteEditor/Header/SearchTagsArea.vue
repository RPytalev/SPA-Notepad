<template>
    <div class="search-area">
        <SearchTagInput @tag-input="tagInput" />
        <SearchTagButton @change-search-tag="changeSearchTag" />
    </div>
</template>

<script>
import SearchTagButton from './SearchTagButton.vue'
import SearchTagInput from './SearchTagInput.vue'

    export default {
        name: 'SearchTagsArea',
        data(){
            return {
                searchTag: ''
            }
        },
        components: {
            SearchTagButton,
            SearchTagInput
        },
        methods: {
            tagInput(searchTag) {
                this.searchTag = searchTag;
            },
            changeSearchTag() {
                this.$emit('change-search-tag', this.searchTag);
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