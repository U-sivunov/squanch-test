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
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
  }

  .v-pagination__list {
    display: none !important;
  }
</style>
