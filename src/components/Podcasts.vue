<script setup>
    import { ref } from 'vue';
    import Episodes from './Episodes.vue'
    import episodes from '../data/site-data'
    const podcasts = ref(episodes)
    const lastListened = ref(null)
    const handleClick = id => {
        lastListened.value = id
        podcasts.value = podcasts.value
                                .map(podcast => podcast.id === id ? 
                                ({...podcast, listened: true}) : podcast)
    }
    const handleShiftClick = id => {
        podcasts.value = podcasts.value.map(podcast => {
            if(!lastListened.value) return podcast
            const [min, max] = [lastListened.value, id].sort((a, b) => a - b)
            if(podcast.id > min && podcast.id < max) podcast.listened = true
            return podcast
        })
    }
    const handleListened = ({ id, eventType }) => {
        if(eventType === 'click') handleClick(id)
        else handleShiftClick(id)
    }
</script>

<template>
    <main>
        <div class="cover-image">
            <img src="/src/assets/podcast-cover.png" alt="podcast-cover-image">
        </div>
        <div class="content">
            <h5>LISTEN TO ALL THE COMPRESSED.FM EPISODES</h5>
            <Episodes :episodes="podcasts" @listened="handleListened" />
        </div>
    </main>
</template>

<style scoped lang="less">
    main{
        display: flex;
        max-width: 1200px;
        width: 90%;
        margin: 0 auto;
        @media(max-width: 1000px){
            flex-direction: column;
            padding: 30px 0;
        }
        
        .cover-image{
            height: 585px;
            filter: drop-shadow(0px 5.40459px 20.4276px #453F3F);
            @media(max-width: 1000px){
                height: auto;
            }
            img{
                width: 100%;
                height: 585px;
                display: block;
                @media(min-width: 600px) and (max-width: 1000px){
                    height: 485px;
                }
                @media(max-width: 600px){
                    height: auto;
                }
            }
        }
        .content{
            border-radius: 0 18px 18px 0;
            padding: 45px;
            flex-grow: 1;
            background-color: #F3F3F3;
            height: 550px;
            align-self: center;
            @media(max-width: 1000px){
                padding: 10px;
                padding-top: 40px;
                height: auto;
                width: 100%;
                border-radius: 0;
            }
            h5{
                color: #A7A7A7;
            }
        }
    }
</style>