<template>
  <header class="header">
    <div class="header__contents">
      <a class="header__logo">
        <img
          class="header__pic"
          src="./icons/android-chrome-192x192.png"
          alt="logo"
        />
      </a>
      <p class="header__name">Gallery</p>
    </div>
  </header>

  <div class="gallery">
    <gallery-poster
      v-for="(poster, index) in gallery"
      :key="poster.id"
      :poster="poster"
      :index="index"
      @maximize-poster="showMaximized"
    ></gallery-poster>
  </div>

  <div v-if="currentPage < lastPage" class="loadmore">
    <button class="loadmore__button" @click="fetchImages">
      ↻ Load more
    </button>
  </div>

  <maximized-poster
    v-if="isMaximized"
    :poster="gallery[activeImageIndex]"
    @hide-maximized="hideMaximized"
  ></maximized-poster>
</template>

<script>
import GalleryPoster from "./components/GalleryPoster.vue";
import MaximizedPoster from "./components/MaximizedPoster.vue";

export default {
  components: {
    GalleryPoster,
    MaximizedPoster
  },
  data() {
    return {
      currentPage: 0,
      lastPage: undefined,
      gallery: [],
      isMaximized: false,
      activeImageIndex: undefined
    };
  },
  computed: {
    fetchUrl() {
      return (
        "https://okolo.city/api/v1/subjects?only_paid=0&page=" +
        this.nextPage +
        "&per_page=6" +
        "&pagination_hash_random=1"
      );
    },
    nextPage() {
      return this.currentPage + 1;
    }
  },
  async mounted() {
    this.fetchImages();
  },
  methods: {
    async fetchImages() {
      const response = await fetch(this.fetchUrl);
      const posters = await response.json();
      console.log(posters);
      this.gallery = this.gallery.concat(posters.data);
      this.lastPage = posters.meta.last_page;
      this.currentPage = posters.meta.current_page;
    },
    showMaximized(index) {
      this.activeImageIndex = index;
      this.isMaximized = true;
    },
    hideMaximized() {
      this.isMaximized = false;
    }
  }
};
</script>

<style lang="scss">
@import "./styles/index.scss";
</style>
