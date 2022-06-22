<template>
  <v-row justify="center">
    <v-col
      cols="3"
      md="4"
      v-for="(image, i) in images"
      :key="i"
    >
      <v-img
        :lazy-src="require('@/assets/imgs/lazy/' + image.filename)"
        :src="require('@/assets/imgs/thumb/' + image.filename)"
        aspect-ratio="1"
        class="rounded-xl"
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
    }
  }
}
</script>

<style>

</style>