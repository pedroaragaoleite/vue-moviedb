<template>
    <div class="movie-detail">
        <h2>{{movie.Title}}</h2>
        <p>{{movie.Year}}</p>
        <img :src="movie.Poster" alt="Movie Poster" class="feature-img">
        <p>{{movie.Plot}}</p>
    </div>
</template>

<script setup>
import { ref, onBeforeMount } from 'vue';
import { useRoute } from 'vue-router';
import env from "@/env.js";

const movie = ref({});
const route = useRoute();

onBeforeMount(() => {
    fetch(`https://www.omdbapi.com/?apikey=${env.apikey}&i=${route.params.id}&plot=full`)
        .then(response => response.json())
        .then(data => {
            movie.value = data;
            console.log(movie.value);
        });
});

</script>

<style lang="scss">
  .movie-detail {
    padding: 16px;
    h2 {
        color: #fff;
        font-size: 28px;
        font-weight: bold;
        margin-bottom: 16px;
    }
    p  {
        color: #fff;
        font-size: 18px;
        line-height: 1.4;
        text-align: center;
    }
    .feature-img {
        display: block;
        max-width: 100%;
        margin: 0 auto;
        margin-bottom: 16px;
        
    }
  }  
</style>