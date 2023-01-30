<script setup>
    import checked from '../assets/checkbox--checked.svg'
    import unchecked from '../assets/checkbox--unchecked.svg'
    defineProps(['episode'])
    const emit = defineEmits(['listened'])
    const handleClick = (id, eventType) => {
        const payload = {
            id,
            eventType
        }
        emit('listened', payload)
    }
</script>

<template>
    <div 
        class="episode"
        @click.shift="() => handleClick(episode.id, 'shiftClick')"
        @click="() => handleClick(episode.id, 'click')"
        >
        <div class="checkmark">
            <img :src="episode.listened ? checked : unchecked" alt="checkmark">
        </div>
        <div :class="episode.listened ? 'episode-content listened' : 'episode-content'">
            <span>{{ episode.id }}</span>
            <span>||</span>
            <span>{{ episode.name }}</span>
        </div>
    </div>
</template>

<style scoped lang="less">
    .episode{
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 10px;
        margin-top: 40px;
        user-select: none;
        .checkmark{
            width: 30px;
            height: 30px;
            img{
                width: 100%;
                height: auto;
            }
        }
        .episode-content{
            color: #4E4E4E;
            font-weight: 700;
            font-size: 14px;
            display: flex;
            gap: 8px;
            position: relative;
            transition: all .5s;
            &:last-child{
                overflow: hidden;
                text-overflow: ellipsis;
                // white-space: nowrap;
                flex-grow: 1;
            }
            @media(max-width: 1000px){
                font-size: 12px;
            }
            @media(max-width: 400px){
                font-size: 10px;
            }
            &::before{
                content: '';
                width: 0;
                height: 2px;
                background-color: #4E4E4E;
                position: absolute;
                left: 0;
                top: 50% - 1;
                transition: all .5s;
            }
            &.listened{
                color: #C9CDD1;
                &::before{
                    width: 100%;
                }
            }
        }
    }
</style>