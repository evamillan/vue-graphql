<template>
<v-dialog v-model="dialog" width="500">
  <template v-slot:activator="{ on }">
    <v-card @click="dialog = true" active-class="movie-card">
      <v-img :src="imageSrc" fill-height>
        <v-container fill-height fluid pa-2>
          <v-layout>
            <v-flex xs12 align-end flexbox>
              <span class="headline white--text" v-text="movie.title"></span>
            </v-flex>
          </v-layout>
        </v-container>
      </v-img>
    </v-card>
  </template>

  <v-card>
    <v-card-title class="headline grey lighten-2" primary-title>
      {{ movie.title }}
    </v-card-title>

    <v-card-text>
      {{ movie.overview }}
    </v-card-text>
  </v-card>
</v-dialog>
</template>

<script>
export default {
  name: 'Movie',

  props: {
    movie: Object,
    images: Object
  },

  data() {
    return {
      dialog: false
    }
  },

  computed: {
    imageSrc: function() {
      return `${this.images.base_url}/${this.images.poster_sizes[3]}/${this.movie.poster_path}`
    }
  }
}
</script>

<style scoped>
.container {
  cursor: pointer;
}

.container:hover {
  background: rgb(0,0,0);
  background: linear-gradient(180deg, rgba(0,0,0,1) 0%, rgba(0,0,0,1) 15%, rgba(0,212,255,0) 80%);
}

.white--text {
  text-shadow: 0px 1px 4px black;
}
</style>
