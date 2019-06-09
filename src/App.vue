<template>
  <div id="app" data-app="true">
    <v-toolbar
      color="purple darken-4"
      dark
      app
      fixed>
      <v-toolbar-title style="width: 300px" class="ml-0 pl-3">
        <span class="hidden-sm-and-down">Movie DB</span>
      </v-toolbar-title>
      <v-text-field
        v-model="query"
        flat
        solo-inverted
        prepend-icon="search"
        label="Search"
      ></v-text-field>
      <v-spacer></v-spacer>
    </v-toolbar>

    <v-content>
      <v-container fluid grid-list-md>
        <v-layout row wrap justify-center>
          <v-flex v-for="movie in movies" :key="movie.id" xs2>
            <movie :movie="movie" :images="config.images"></movie>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </div>
</template>

<script>
import gql from 'graphql-tag';
import Movie from './components/Movie.vue'

export default {
  name: 'App',
  data() {
    return {
      movies: [],
      config: {},
      query: ''
    }
  },

  apollo: {
    movies: {
      query: gql`query movies($query: String!) {
        movies(query: $query) {
          id
          title
          overview
          poster_path
        }
      }`,
      variables () {
        return {
          query: this.query,
        }
      }
    },
    config: {
      query: gql` {
        config {
          images {
            base_url
            poster_sizes
          }
        }
      }`
    }
  },

  components: {
    Movie
  }
}
</script>

<style>
#app {
  font-family: 'Roboto', Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
