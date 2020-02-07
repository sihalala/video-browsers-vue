<template>
    <div class="container">
        <SearchBar @termChange="onTermChange"></SearchBar>
<!--        v-bind === :-->
        <div class="row">
            <VideoDetail v-bind:video="selectedVideo"></VideoDetail>
            <VideoList @videoSelect="onVideoSelect" :videos="videos"></VideoList>
        </div>

    </div>
</template>

<script>
    import SearchBar from "./components/SearchBar";
    import VideoList from "./components/VideoList";
    import VideoDetail from "./components/VideoDetail";
    import axios from 'axios';
    const API_KEY = "AIzaSyDH2Jf0MBISKY1P_-puj0dG26jsUGehIgM";

    export default {
        name: "App",
        data(){
            return { videos: [],selectedVideo:null}
        },
        components: {
            SearchBar,
            VideoList,
            VideoDetail
        },
        methods: {
            onTermChange(term){
                axios.get('https://www.googleapis.com/youtube/v3/search',{
                    params: {
                        key: API_KEY,
                        type: 'video',
                        part: 'snippet',
                        q: term
                    }
                }).then(response =>{
                    console.log(response);
                    this.videos = response.data.items;

                });
            },
            onVideoSelect(video){
                this.selectedVideo = video;
            }
        }
    }
</script>

<style scoped>

</style>