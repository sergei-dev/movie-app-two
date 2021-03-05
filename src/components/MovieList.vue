<template>
  <div class="list-wrap">
    <div class="list">
      <MovieItem
        v-for="(movie, index) in movies"
        :title="movie.title"
        :poster_path="movie.poster_path"
        :isShowBtnInfo="true"
        :count="movie.count"
        :overview="movie.overview"
        :id="movie.id"
        :index="index"
        :key="movie.id"
        v-on:show-popup="showPopup"
        v-on:show-movie="openCurrentItem"
      />
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import ButtonComponent from "@/components/ButtonComponent.vue";
import MovieItem from "@/components/MovieItem.vue";

export default Vue.extend({
  name: "MovieList",
  components: {
    ButtonComponent,
    MovieItem,
  },
  props: {
    movies: Array,
  },
  methods: {
    showPopup() {
      this.$emit("show-popup", true);
    },
    openCurrentItem(currentItem: object) {
      console.log(currentItem);
      this.$emit("show-movie", currentItem);
    }
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.list-wrap {
  padding: 3vw 0;
  display: flex;
  justify-content: center;
}

.list {
  display: flex;
  flex-wrap: wrap;
  margin: -1vw;
  max-width: 1500px;
}
</style>
