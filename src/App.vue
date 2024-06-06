<script>
import SearchMovies from './components/SearchMovies.vue';
import axios from 'axios';
import { store } from './store'



export default {
  name: 'App',
  components: {
    SearchMovies,
  },
  data() {
    return {
      store,
      axios
    }
  },
  methods: {
    onSearch(inputText) {
      console.log(inputText)
      console.log(store.results)


      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=8a3b83078838507514062cfc870ff804&query=${inputText}&language=it-IT`).then((response) => {
        this.store.resultsMovie = response.data.results;

      });
      axios.get(`https://api.themoviedb.org/3/search/tv?api_key=8a3b83078838507514062cfc870ff804&query=${inputText}&language=it-IT`).then((response) => {
        this.store.resultsTv = response.data.results;

      });

      // const filteredResults = store.results.filter((result) =>
      //   result.original_title.toLowerCase().includes(inputText.toLowerCase()) || result.title.toLowerCase().includes(inputText.toLowerCase()) || result.original_language.toLowerCase().includes(inputText.toLowerCase()) || result.original_language.toLowerCase().includes(inputText.toLowerCase()) || result.vote_average.toString().includes(inputText))
      // console.log(filteredResults);
      // store.results = filteredResults;
    },
  },
  created() {

  }
};


</script>

<template>
  <div id="app">
    <SearchMovies @search-event="onSearch" />
  </div>
</template>



<style lang="scss">
@use './assets/scss/main.scss' as *;

body {
  background-color: '$body-bg-color';
}
</style>
