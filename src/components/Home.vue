<template>
  <div>
    <div :style="bannerProps" v-if="bgLoaded">
      <div :style="logoProps">
        <v-card
          v-if="!showGalleries"
          color="rgb(0,0,0,.5)"
        >
          <v-card-title
            v-if="$vuetify.breakpoint.mdAndUp"
            :style="nameProps"
          >
            Zero-One Photography
          </v-card-title>
          <v-card-title
            :style="nameProps"
            v-else
          >
            <v-row justify="center">
              <v-col cols="12" class="text-center pb-0">
                Zero-One
              </v-col>
              <v-col cols="12" class="text-center pt-0">
                Photography
              </v-col>
            </v-row>
          </v-card-title>
          <v-divider dark></v-divider>
          <v-card-actions>
            <v-row justify="center">
              <v-col cols="12" md="4" class="d-flex justify-center pb-md-3 pb-0" >
                <v-btn 
                  outlined 
                  rounded 
                  color="white"
                  @click="showGalleries = !showGalleries"
                >
                  Galleries
                </v-btn>
              </v-col>
              <v-col cols="2" class="py-md-3 py-2 d-flex justify-center">
                <v-btn
                  color="white"
                  icon
                  href="https://www.instagram.com/zero_821/"
                  target="_blank"
                >
                  <v-icon>
                    fab fa-instagram
                  </v-icon>
                </v-btn>
              </v-col>
              <v-col cols="2" class="py-md-3 py-2 d-flex justify-center">
                <v-btn
                  color="white"
                  icon
                  href="https://www.facebook.com/deckera"
                  target="_blank"
                >
                  <v-icon>
                    fab fa-facebook
                  </v-icon>
                </v-btn>
              </v-col>
            </v-row>
          </v-card-actions>
        </v-card>
      </div>

      <v-slide-y-reverse-transition>
        <div :style="galleriesProps" v-if="showGalleries">
            <galleries @collapse="showGalleries = !showGalleries"/>
        </div>
        </v-slide-y-reverse-transition>

    </div>

    <v-row v-if="!bgLoaded" :style="loadingProps">
      <v-col cols="12" class="d-flex justify-center">
        <v-progress-linear
          indeterminate
        >
        </v-progress-linear>
      </v-col>
    </v-row>

  </div>
  
</template>

<script>
  import Galleries from "./Galleries.vue"; 
  export default {
    components: { 
      Galleries 
    },
    data() {
      return {
        showGalleries: false,
        bgLoaded: false,
        bannerProps: {
          backgroundImage: `url(${require('@/assets/imgs/banner/64.jpg')})`,
          backgroundSize: 'cover',
          height: '100vh',
          width: '100vw'
        },
        loadingProps: {
          position: 'absolute',
          top: '50%',
          left: '50%',
          transform: 'translate(-50%, -50%)',
          minWidth: '100px',
          width: '400px'
        },
        logoProps: {
          position: 'absolute',
          top: '50%',
          left: '50%',
          transform: 'translate(-50%, -50%)',
        },
        nameProps: {
          fontFamily: 'Rajdhani, sans-serif',
          color: 'white',
          fontSize: '1.4rem'
        },
        galleriesProps: {
          height: '100vh',
          width: '100vw',
          backgroundColor: 'white'
        }
      }
    },
    computed: {
      viewPortSize() {
        return {
          xsOnly: this.$vuetify.breakpoint.xsOnly,
          smOnly: this.$vuetify.breakpoint.smOnly,
          mdOnly: this.$vuetify.breakpoint.mdOnly,
          lgAndUp: this.$vuetify.breakpoint.lgAndUp
        };
      }
    },
    watch: {
      viewPortSize: {
        handler: function (val) {
          this.updateBackgroundImage(val);
        },
        deep: true
      }
    },
    created() {
      const breakpoints = {
        xsOnly: this.$vuetify.breakpoint.xsOnly,
        smOnly: this.$vuetify.breakpoint.smOnly,
        mdOnly: this.$vuetify.breakpoint.mdOnly,
        lgAndUp: this.$vuetify.breakpoint.lgAndUp
      };
      this.updateBackgroundImage(breakpoints);
      this.loadBg();
    },
    methods: {
      updateBackgroundImage(breaks) {
        if (breaks.xsOnly) {
          this.bannerProps.backgroundImage = `url(${require('@/assets/imgs/banner/64.jpg')})`;
          this.nameProps.fontSize = '1.4rem';
        } else if (breaks.mdOnly || breaks.smOnly) {
            this.bannerProps.backgroundImage = `url(${require('@/assets/imgs/banner/Z72_2804.jpg')})`;
            if (breaks.mdOnly) {
              this.nameProps.fontSize = '2.5rem';
            } else if (breaks.smOnly) {
                this.nameProps.fontSize = '1.7rem';
            }
        } else if (breaks.lgAndUp) {
          this.bannerProps.backgroundImage = `url(${require('@/assets/imgs/banner/68.jpg')})`;
          this.nameProps.fontSize = '3rem';
        }
      },
      loadBg() {
        const image = new Image();
        const that = this;
        image.onload = function () {
          that.bgLoaded = !that.bgLoaded;
        }
        image.src = require('@/assets/imgs/banner/68.jpg');
      }
    },

  }
</script>
