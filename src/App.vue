<template>
  <h1>The Rick and Morty</h1>
  <CharactersList/>
</template>

<script>
  import CharactersList from "@/components/CharactersList";

  export default {
    name: 'App',
    components: {
      CharactersList,
    },
  }
</script>

<style>
  html {
    font: 112.5% / 1.625 -apple-system, 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'Helvetica', 'Arial', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
  }

  body {
    margin: 0;
  }

  #app {
    font-family: -apple-system, 'BlinkMacSystemFont', 'Segoe UI', 'Roboto', 'Helvetica', 'Arial', sans-serif, 'Apple Color Emoji', 'Segoe UI Emoji', 'Segoe UI Symbol';
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
  }

  .v-pagination__list {
    display: none !important;
  }

  h1 {
    font-size: 5.625rem;
    font-weight: 900;
    margin: 0;
  }
</style>
