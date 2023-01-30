<script setup>
    import Episode from './Episode.vue'
    defineProps(['episodes'])
    const emit = defineEmits(['listened'])
    const handleListened = payload => emit('listened', payload)
</script>

<template>
    <div class="episodes">
        <Episode 
        v-for="episode in episodes" 
        :episode="episode" 
        :key="episode.id"
        @listened="handleListened"
        />
    </div>
</template>

<style scoped lang="less">
    .episodes{
        max-height: 460px;
        overflow-y: scroll;
        &::-webkit-scrollbar{
            width: 5px;
        }
        &::-webkit-scrollbar-track{
            background-color: transparent;
            border-radius: 50px;
        }
        &::-webkit-scrollbar-thumb{
            background-color: #9b9898;
            border-radius: 50px;
            cursor: pointer;
            &:hover{
                background-color: rgb(184, 179, 179);
            }
        }
    }
</style>