<template>
  <div id="app">
    <MovieList v-on:show-popup="showPopup" :movies="movies" />
    <Popup v-on:show-popup="showPopup" v-if="isVisiblePopup">
       <MovieItem
          :title="this.movies[this.movieIndex].title"
          :overview="this.movies[this.movieIndex].overview"
          :poster_path="this.movies[this.movieIndex].poster_path"
          :count="this.movies[this.movieIndex].count"
          :id="this.movies[this.movieIndex].id"
          :isFullScreenView="true"
          :isShowBtnInfo="false"
        />
    </Popup>
  </div>
</template>

<script lang="ts">
import axios from "axios";
import Vue from "vue";
import MovieList from "./components/MovieList.vue";
import MovieItem from "./components/MovieItem.vue";
import Popup from "./components/Popup.vue";

export default Vue.extend({
  name: "App",
  components: {
    MovieList,
    MovieItem,
    Popup,
  },
  data() {
    return {
      movies: [],
      isVisiblePopup: false,
      movieIndex: Number
    };
  },
  mounted() {
    axios
      .get(
        "https://api.themoviedb.org/3/movie/popular?api_key=331809dfe739c8b14228e31bcaf71859"
      )
      .then((response) => {
        this.movies = response.data.results;
      })
      .catch((error) => {
        console.log(error);
      })
      .finally(() => console.log("finally"));
  },
  methods: {
    showPopup(isVisible: boolean, movieIndex: number) {
      this.isVisiblePopup = isVisible;
      if (movieIndex) {
        this.movieIndex = movieIndex
        console.log(movieIndex)
      }
    },
  },
});
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
</style>
