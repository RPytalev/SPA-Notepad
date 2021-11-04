<template>
    <div class="tags-list">
        <div class="tags" :key="item.id" v-for="item in tagsList">
            <Tag :tagsList="tagsList" :item="item" />
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
            tagsList: Array
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