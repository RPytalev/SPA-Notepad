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
                searchTag: '',
                event: {}
            }
        },
        components: {
            SearchTagButton,
            SearchTagInput
        },
        methods: {
            tagInput(searchTag, event) {
                this.searchTag = searchTag;
                this.event = event;
            },
            changeSearchTag() {
                this.$emit('change-search-tag', this.searchTag);
                this.event.target.value = '';
            }
        }
    }
</script>

<style lang="sass" scoped>
.search-area
    display: flex
    justify-content: center
    align-items: center
</style>