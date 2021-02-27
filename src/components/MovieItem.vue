<template>
  <div class="item" :class="{ full: isFullScreenView }">
    <div class="item__inner">
      <div class="item__img-wrap" v-if="poster_path">
        <img
          :src="'https://image.tmdb.org/t/p/original' + poster_path"
          alt=""
          class="item__img"
        />
      </div>
      <div class="item__head">
        <h3 class="item__name">{{ title }}</h3>
      </div>
      <p class="item__descr">{{ overview }}</p>
      <div class="item__count-wrap">
        <button class="item__counter" @click="countReduce()">-</button>
        <span class="item__count-text">{{ count }}</span>
        <button class="item__counter" @click="countEnlarge()">+</button>
      </div>
      <div class="item__bottom" v-if="isShowBtnInfo">
        <ButtonComponent :text="buttonText" v-on:click.native="$emit('show-popup', index)"/>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import ButtonComponent from "@/components/ButtonComponent.vue";

export default Vue.extend({
  name: "MovieItem",
  components: {
    ButtonComponent,
  },
  props: {
    id: Number,
    index: Number,
    title: String,
    overview: String,
    poster_path: String,
    isShowBtnInfo: Boolean,
    isFullScreenView: Boolean,
  },
  data() {
    return {
      buttonText: "Информация",
      count: 1,
    };
  },
  methods: {
    countReduce() {
      if (this.count >= 1) {
          this.count--;
      }
    },
    countEnlarge() {
      this.count++;
    },
  },
});
</script>

<style scoped lang="scss">
.item {
  width: calc(100% / 3);
  display: flex;
  padding: 1vw;

  &.full {
    width: 70%;
    padding: 0;
  }

  &__img-wrap {
    width: 100%;
    position: relative;
    padding-bottom: 60%;
    margin-bottom: 1vw;
    border: 1px solid gray;
  }

  &__img {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    object-fit: cover;
  }

  &__inner {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    border: 1px solid tomato;
    padding: 1vw;
  }

  &__descr {
    margin-bottom: 2vw;
  }

  &__bottom {
    margin-top: auto;
    padding-top: 1vw;
  }

  &__count-wrap {
    margin-top: auto;
    display: flex;
    align-items: center;
  }

  &__counter {
    display: inline-block;
    border-radius: 50%;
    width: 30px;
    height: 30px;
    padding: 0.4vw;
    border: 1px solid gray;
    cursor: pointer;
    background: 0 0;
  }

  &__count-text {
    display: block;
    margin: 0 0.5vw;
  }
}
</style>
