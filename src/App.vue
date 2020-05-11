<template>
  <div id="app">
    <main>
      <div class="header">
        <img class="header__logo" src="./assets/logo.png">
        <div class="header__text">
          <h1>Movie Database</h1>
          <p>v1.0.0</p>
        </div>
      </div>
      <div class="search">
        <label>Search for movies by title:</label>
        <input
          type="text"
          placeholder="Enter the title of a movie"
          v-model="query"
          v-bind:class="searchError ? 'input--error' : ''"
           />
        <button v-on:click="fetchMovie">Search</button>
        <p v-if="searchError" class="error">Please enter a movie title to search</p>
      </div>
      <loading v-if="loading" />
      <section v-if="loaded" class="results">
        <movieResult
          v-for="(movie, index) in movies"
          v-bind:key="movie.Title+index"
          v-bind:movie="movie"
        ></movieResult>
      </section>
      <toTop />
    </main>
  </div>
</template>

<script>
  import movieResult from './components/movieResult';
  import loading from './components/loading';
  import toTop from './components/toTop';

  export default {
    name: 'App',
    components: {
      movieResult,
      loading,
      toTop
    },
    data() {
      return {
        api_url: 'https://movie-database-imdb-alternative.p.rapidapi.com/',
        query: '',
        movies: [],
        searchError: false,
        loaded: false,
        loading: false
      }
    },
    methods: {
      fetchMovie: function() {
        if (this.query) {
          // Clear movie array.
          this.movies = [];
          // Set props to show/hide loading states or errors.
          this.loading = true;
          this.loaded = false;
          this.searchError = false;
          // remove spaces from movie name and encode
          let formattedMovieName = encodeURIComponent(this.query.trim())
          // fetch api
          fetch(`${this.api_url}?r=json&s=${formattedMovieName}&type=movie`, {
            "method": "GET",
            "headers": {
              "x-rapidapi-host": "movie-database-imdb-alternative.p.rapidapi.com",
              "x-rapidapi-key": "87cd541c16msh01a954c6070da2fp1d5a57jsn4f43f3512649"
            }
          })
          .then(res => {
            // update loading states
            this.loading = false;
            this.loaded = true;
            return res.json();
          })
          .then(this.setResults);
        }
        else {
          this.searchError = true
        }
      },
      setResults(results) {
        // store results
        this.movies.push(...results.Search);
      }
    }
    
  }
</script>

<style lang="scss">
  @import "styles/index.scss";
</style>