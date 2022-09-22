<template>
  <div class="home">
    <div class="feature-card">
      <router-link to="/movie/tt2536128">
        <img src="../assets/pinnochio.jpg" alt="Pinnochio Poster Movie" class="feature-img">
        <div class="detail">
          <h3>Pinnochio</h3>
          <p>A magical log falls off a wagon, stopping at Geppetto's door. The wood carver creates a puppet from the log and names it Pinocchio. Pinocchio comes to life and runs away in the streets, turning the town upside down. The carpenter is blamed and taken to prison by the carabinieri, while Pinocchio escapes.</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="searchMovies()"  class="search-box">
      <input type="text" name="" id="" placeholder="What are you looking for?" v-model="search">
      <input type="submit" value="Search">
    </form>

    <div class="movies-list">
      <div class="movie" v-for="movie in movies" :key="imdbID">
        <router-link :to="'/movie/' + movie.imdbID" class="movie-link">
          <div class="product-img">
            <img :src="movie.Poster" alt="Movie Poster">
            <div class="type">{{movie.Type}}</div>
          </div>
          <div class="detail">
            <p class="year">{{movie.Year}}</p>
            <h3 class="title">{{movie.Title}}</h3>
          </div>
        </router-link>
        
      </div>
    </div>
  </div>
  
  </template>



<script>

import { ref } from 'vue';
import env  from '@/env.js';

export default {
  setup () {
    const search = ref("");
    const movies = ref([]);

    const searchMovies = () => {
      if(search.value != '') {
        fetch(`https://www.omdbapi.com/?i=tt3896198&apikey=${env.apikey}&s=${search.value}`)
          .then(response => response.json())
          .then(data => {            
            movies.value = data.Search;
            console.log(movies.value);
            search.value = "";
          });
      }
    }

    return {
      search,
      movies,
      searchMovies
    }
  }
}

  


</script>

<style lang="scss">
  .home {
    .feature-card {
      position: relative;
      .feature-img {
        display: block;
        width: 100%;
        height: 400px;
        object-fit: cover;

        position: relative;
        z-index: 0;
        }
      .detail {
        background-color: rgba(0, 0, 0, .6);
        position: absolute;
        left: 0;
        right: 0;
        bottom: 0;
        padding: 16px;
        z-index: 1;
        h3 {
          color: #fff;
          margin-bottom: 16px;
        }
        p {
          color: #fff;

        }
      }
    }
    .search-box {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      padding: 16px;
      input {
        display: block;
        appearance: none;
        border: none;
        outline: none;
        background: none;
        &[type="text"] {
          width: 100%;
          color: #fff;
          background-color: #496583;
          font-size: 20px;
          padding: 10px 16px;
          border-radius: 8px;
          margin-bottom: 15px;
          transition: 0.4s;

          &::placeholder {
            color: #f3f3f3;
          }
          &:focus {
            box-shadow: 0px 3px 6px rgba(0, 0, 0, .2);
          }
        }
        &[type="submit"] {
          width: 100%;
          max-width: 300px;
          background-color: #42B883;
          padding: 16px;
          border-radius: 8px;
          color: #fff;
          font-size: 20px;
          text-transform: uppercase;
          transition: 0.4s;
          &:active {
            background-color: #3B8070;
          }
        }
      }
    }
    .movies-list {
      display: flex;
      flex-wrap: wrap;
      margin: 0px 8px;
      .movie {
        max-width: 50%;
        flex: 1 1 50%;
        padding: 16px 8px;
      }
      .movie-link {
        display: flex;
        flex-direction: column;
        height: 100%;
      }
      .product-img {
        position: relative;
        display: block;
        img {
          display: block;
          width: 100%;
          height: 275px;
          object-fit: cover;
        }
        .type {
          position: absolute;
          padding: 8px 16px;
          background-color: #42B883;
          color: #fff;
          bottom: 16px;
          left: 0;
          text-transform: capitalize;
        }
      }
      .detail {
        background-color: #496583;
        padding: 16px 8px;
        flex: 1 1 100%;
        border-radius: 0px 0px 8px 8px;
        .year {
          color: #fff;
          font-size: 14px;
        }
        .title {
          color: #fff;
          font-weight: bold;
          font-size: 18px;
        }
      }
    }
}

@media only screen and (min-width: 768px) {
  .movie {
    flex:content;
  }
}
</style>
