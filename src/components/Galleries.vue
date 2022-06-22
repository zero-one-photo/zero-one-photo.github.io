<template>
  <v-container>
    <v-row justify="center" class="grey lighten-3 rounded-lg mt-md-5">
      <v-col cols="2" md="1" class="d-flex justify-center align-center pr-0">
        <v-btn
          icon
          elevation="3"
          @click="collapse"
          large
          class="back-button"
        >
          <v-icon>fas fa-chevron-left</v-icon>
        </v-btn>
      </v-col>
      <v-col cols="10" md="11">
        <v-tabs v-model="selectedTab" 
          fixed-tabs
          background-color="grey lighten-3"
          show-arrows
        >
          <v-tab v-for="(tab, t) in tabs" :key="t">
            {{tab}}
          </v-tab>
        </v-tabs>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <grid :selectedTab="selectedTab"/>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Grid from './Grid.vue';
export default {
  components: {
    Grid
  },
  data () {
    return {
      tabs: ['People', 'Animals', 'Street', 'Landscapes'],
      selectedTab: 0,
      showTabArrows: true
    }
  },
  methods: {
    collapse() {
      this.$emit('collapse');
    }
  }
}
</script>

<style scoped>
  .back-button {
    background-color: white;
  }
  .v-tab, .v-tab--active {
    font-size: 1.05rem;
  }
</style>