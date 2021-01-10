<template>
  <div class="gallery__poster" @click="maximize">
    <img class="gallery__img" :src="poster.preview" />
  </div>
</template>

<script>
export default {
  props: {
    poster: {
      type: Object,
      required: true
    },
    index: {
      type: Number,
      required: true
    }
  },
  emits: ["maximize-poster"],
  data() {
    return {};
  },
  methods: {
    maximize() {
      const index = this.index;
      console.log(index);
      this.$emit("maximize-poster", index);
    }
  }
};
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
