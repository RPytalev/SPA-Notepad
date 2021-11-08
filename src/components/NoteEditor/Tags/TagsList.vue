<template>
    <div class="tags-list">
        <div class="tags" :key="item.id" v-for="item in note.tags">
            <Tag 
            :tag="item" 
            :tagDisplayState="tagDisplayState" />
        </div>
    </div>
    
</template>

<script>

import Tag from './Tag.vue'

    export default {
        name: 'TagsList',
        components: {
            Tag
        },
        props: {
            note: Object,
            tagDisplayState: Boolean
        }
    }
</script>

<style lang="sass" scoped>
::-webkit-scrollbar
  width: 0

.tags-list
    display: flex
    flex-flow: row nowrap
    width: 100%
    height: 100%
    overflow: auto

    .tags
        display: flex
        flex-flow: row wrap
        width: 100%
        height: 100%
        background-color: #ff5800
</style>