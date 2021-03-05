<template>
  <div id="app">
    <MovieList v-on:show-popup="showPopup" v-on:show-movie="openCurrentItem" :movies="movies" />
    <Popup v-on:show-popup="showPopup" v-if="isVisiblePopup">
       <MovieItem
          :title="this.currentItem.title"
          :overview="this.currentItem.overview"
          :poster_path="this.currentItem.poster_path"
          :count="this.currentItem.count"
          :id="this.currentItem.id"
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
      currentItem: Object
    };
  },
  mounted() {
    axios
      .get(
        "https://api.themoviedb.org/3/movie/popular?api_key=331809dfe739c8b14228e31bcaf71859"
      )
      .then((response) => {
        const result = response.data.results;
         result.forEach((item: { [x: string]: number; }) => {
          item['count'] = 1;
        })
        this.movies = result;
      })
      .catch((error) => {
        console.log(error);
      })
      .finally(() => console.log("finally"));
  },
  methods: {
    showPopup(isVisible: boolean) {
      this.isVisiblePopup = isVisible;
    },
    openCurrentItem(currentItem: object) {
      this.currentItem = currentItem;
    }
  },
  computed: {
    // getCurrentMovie: {

    // }
  }
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
