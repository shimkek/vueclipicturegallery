<template>
    <div class="gallery__poster" @click="maximize">
    <img class="gallery__img" :src="this.poster.preview">
    </div>
</template>

<script>
export default {
  props: {
    poster: {}
  },
  data () {
    return {
    }
  },
  methods: {
    maximize () {
      const poster = {
        name: this.poster.name,
        coordinates: this.poster.coordinates_geo_object,
        district: this.poster.district,
        src: this.poster.preview
      }
      console.log(poster)
      this.$emit('maximize-poster', poster)
    }
  }
}
</script>

<style lang="scss">
.gallery__poster {
  cursor: pointer;
  width: 480px;
  height: 270px;
  margin: 20px;
  box-shadow: 4px 4px 20px;
  box-sizing: border-box;
}
.gallery__img {
  width: inherit;
  object-fit: contain;
}
</style>
