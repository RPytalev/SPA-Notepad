<template>
    <div class="search-area">
        <SearchInputTag @mouseleave-input-tag="sendInputTag" />
        <SearchNoteBtn @btn-click-search="searchNote" />
    </div>
</template>

<script>
import SearchNoteBtn from './SearchNoteBtn.vue'
import SearchInputTag from './SearchInputTag.vue'

    export default {
        name: 'SearchTagsArea',
        data(){
            return {
                searchTag: '',
                event: {}
            }
        },
        components: {
            SearchNoteBtn,
            SearchInputTag
        },
        methods: {
            sendInputTag(searchTag, event) {
                this.searchTag = searchTag;
                this.event = event;
            },
            searchNote() {
                this.$emit('btn-click-search', this.searchTag);
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