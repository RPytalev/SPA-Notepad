<template>
    <div class="tagslist">
        <div :key="item.id" v-for="item in note.tags">
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
.tagslist
    display: flex
    flex-flow: row wrap
</style>