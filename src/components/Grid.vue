<template>
  <v-row justify="center">
    <v-col
      cols="3"
      md="4"
      v-for="(image, i) in images"
      :key="i"
      class="greyscale"
    >
      <v-img
        :lazy-src="require('@/assets/imgs/lazy/' + image.filename)"
        :src="require('@/assets/imgs/thumb/' + image.filename)"
        aspect-ratio="1"
        class="rounded-xl"
        @click="openCarousel(i)"

      >
        <template v-slot:placeholder>
          <v-row
            class="fill-height ma-0"
            align="center"
            justify="center"
          >
            <v-progress-circular
              indeterminate
              color="grey lighten-5"
            ></v-progress-circular>
          </v-row>
        </template>
      </v-img>
    </v-col>
    <v-dialog 
      v-model="showCarousel"
      eager
    >
      <v-carousel 
        v-model="selectedImage"
        hide-delimiters
        show-arrows-on-hover
        height="auto"
      >
        <v-carousel-item 
          v-for="image in images" 
          :key="image.id"
        >
          <v-img
            :lazy-src="require('@/assets/imgs/thumb/' + image.filename)"
            :src="require('@/assets/imgs/fullsize/' + image.filename)"
            contain
            max-height="1200"
            eager
          >
            <template v-slot:placeholder>
              <v-row
                class="fill-height ma-0"
                align="center"
                justify="center"
              >
                <v-progress-circular
                  indeterminate
                  color="grey lighten-5"
                ></v-progress-circular>
              </v-row>
            </template>
          </v-img>
        </v-carousel-item>
      </v-carousel>

    </v-dialog>
  </v-row>
</template>

<script>
export default {
  props: ['selectedTab'],
  watch: {
    selectedTab: function () {
      switch (this.selectedTab) {
        case 0: 
          this.images = require('@/assets/json/people.json');
          break;
        case 1: 
          this.images = require('@/assets/json/animals.json');
          break;
        case 2: 
          this.images = require('@/assets/json/street.json');
          break;
        case 3: 
          this.images = require('@/assets/json/landscapes.json');
          break;
        default:
          this.images = require('@/assets/json/people.json');
          break;
      }
    }
  },
  data () {
    return {
      images: require('@/assets/json/people.json'),
      selectedImage: 0,
      showCarousel: false,
    }
  },
  methods: {
    openCarousel(image) {
      this.selectedImage = image;
      this.showCarousel = true;
    }
  }
}
</script>

<style scoped>
  .greyscale {
    filter: grayscale(100%);
  }
  .greyscale:hover {
    filter: grayscale(0%);
    transition: 0.5s ease;
    cursor: pointer;
  }
</style>