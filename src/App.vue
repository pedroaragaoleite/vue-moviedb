<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>    
        <RouterLink to="/">
          <h1><span>Vue</span>Movies</h1>
        </RouterLink>
  </header>
  <main>
    <RouterView />
  </main>
</template>

<style lang="scss">
  * {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: "Fira Sans", sans-serif;
    &::selection {
      background: transparentize(#42B883, 0.5)
    }
  }

  body {
    background-color: #35495E;
  }

  a {
    text-decoration: none;
  }

  img {
    max-width: 100%;
  }

  header {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 10px 16px;
    background-color: #2C3D4E;
    box-shadow: 0px 0px 6px rgba(0, 0, 0, .1);

    h1 {
      color: #fff;
      font-size: 20px;
      span {
        color: #42B883;
      }
    }
  }
</style>
