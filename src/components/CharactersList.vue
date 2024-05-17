<template>
  <div class="filter-row">
      <label>Filter by name:</label>
      <input v-model="state.nameFilter">
      <label>Filter by status:</label>
      <select v-model="state.statusFilter">
        <option value="" selected></option>
        <option>Alive</option>
        <option>Dead</option>
        <option>Unknown</option>
      </select>
    <button @click="applyFilters">Apply</button>
  </div>
  <PaginationBar v-model="state.page"
                 :total-row="state.totalCount" :align="'center'" :page-size-menu="[20]"
                 @change="changePage">
  </PaginationBar>
  <div class="list">
    <div v-for="character in state.list" v-bind:key="character.id">
      <CharacterCard :character="character"/>
    </div>
    <h4 v-if="!state.list.length">Nothing found...</h4>
  </div>
</template>

<script>
  import CharacterCard from "@/components/CharacterCard";
  import PaginationBar from "v-page";
  import {reactive} from "vue"
  import axios from "axios"
  import lodash from "lodash"

  export default {
    name: 'CharactersList',
    components: {
      CharacterCard,
      PaginationBar
    },
    setup() {
      let episodeNameById;
      const state = reactive({
        list: [],
        page: 1,
        totalCount: 1,
        nameFilter: '',
        statusFilter: '',
      });
      const getCharactersPage = () => {
        const params = {
          page: state.page,
          name: state.nameFilter,
          status: state.statusFilter,
        }
        axios
          .get(`https://rickandmortyapi.com/api/character`, {params})
          .then((response) => {
            state.list = response.data.results;
            state.totalCount = response.data.info.count;
            fillFirstSeenInFields()
          })
          .catch(() => {
            state.list = [];
            state.totalCount = 0;
          });
      }
      const applyFilters = () => {
        state.page = 1;
        getCharactersPage();
      }
      const changePage = (data) => {
        state.page = data.pageNumber;
        getCharactersPage();
      }
      const fillFirstSeenInFields = () => {
        const firstSeenEpisodes = lodash.map(state.list, getFirstEpisodeIdFromCharacter);
        const uniqueFirstSeenEpisodesId = lodash.uniq(firstSeenEpisodes);
        axios
          .get(`https://rickandmortyapi.com/api/episode/${uniqueFirstSeenEpisodesId}`)
          .then((response) => {
            const firstSeenEpisodesNames = lodash.map(response.data, 'name');
            episodeNameById = lodash.zipObject(uniqueFirstSeenEpisodesId, firstSeenEpisodesNames);
            state.list = lodash.map(state.list, addFirstEpisodeName);
          });
      }

      const addFirstEpisodeName = (character) => {
        return lodash.assign({}, character, {firstEpisodeName: episodeNameById[getFirstEpisodeIdFromCharacter(character)]});
      }

      const getFirstEpisodeIdFromCharacter = (character) => {
        return character.episode[0].split('/').pop()
      }

      getCharactersPage();
      return {state, applyFilters, changePage};
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .list {
    display: flex;
    -webkit-box-pack: center;
    justify-content: center;
    -webkit-box-align: center;
    align-items: center;
    flex-wrap: wrap;
    max-width: 1920px;
    background: rgb(39, 43, 51);
    margin-top: 4px;
  }

  .filter-row {
    display: flex;
    flex-direction: row;
    justify-content: center;
    gap: 10px;
    align-items: stretch;
    margin-bottom: 4px;
  }

</style>
