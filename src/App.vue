<template>
    <header class="header">
        <div class="header__contents">
            <a class="header__logo" href="./index.html">
                <img class="header__pic" src="./icons/android-chrome-192x192.png" alt="logo">
            </a>
            <p class="header__name">Gallery</p>
        </div>
    </header>

    <div class="gallery" :class="{gallery_minimized : isMaximized}">
        <gallery-poster v-for="(poster, index) in gallery" :poster="poster" :key="index" @maximize-poster="showMaximized"></gallery-poster>
    </div>

    <div class="loadmore" :class="{loadmore_minimized : isMaximized}">
        <button class="loadmore__button" @click="fetchImages">
            ↻ Load more
        </button>
    </div>

    <maximized v-if="isMaximized" :poster="maximizedPoster" @hide-maximized-event="hideMaximized"></maximized>

</template>

<script>
import GalleryPoster from './components/GalleryPoster.vue'
import Maximized from './components/Maximized.vue'

export default {
  data () {
    return {
      pictureQuntity: 0,
      page: 0,
      gallery: [],
      isMaximized: false,
      maximizedPoster: {
        name: null,
        district: null,
        coordinates: null,
        src: null
      }
    }
  },
  methods: {
    async fetchImages () {
      this.page++
      this.pictureQuntity = this.pictureQuntity + 6
      const response = await fetch(this.fetchUrl)
      const posters = await response.json()
      console.log(posters)
      for (let i = 0; i < posters.data.length; i++) {
        this.gallery.push(posters.data[i])
      }
    },
    showMaximized (poster) {
      this.maximizedPoster.name = poster.name
      this.maximizedPoster.coordinates = poster.coordinates
      this.maximizedPoster.district = poster.district
      this.maximizedPoster.src = poster.src
      this.isMaximized = true
    },
    hideMaximized () {
      this.isMaximized = false
    }
  },
  computed: {
    fetchUrl () {
      return 'https://okolo.city/api/v1/subjects?only_paid=0&page=' + this.page + '&per_page=6' + '&pagination_hash_random=1'
    }
  },
  async mounted () {
    this.fetchImages()
  },
  components: {
    GalleryPoster,
    Maximized
  }
}
</script>

<style lang="scss">
@import './styles/index.scss';
</style>
