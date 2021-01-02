<template>
     <div class="maximized">
        <button class="maximized__close-button" @click="$emit('hide-maximized-event')">×</button>
        <img :src="this.poster.src" class="maximized__img">
        <p class="maximized__text">Name:<span class="maximized__text_aligned-right"> {{poster.name}}</span></p>
        <p class="maximized__text">Coordinates:<span class="maximized__text_aligned-right">{{poster.coordinates}}</span></p>
        <p class="maximized__text">District:<span class="maximized__text_aligned-right">{{poster.district}}</span></p>
    </div>
</template>

<script>
export default {
  props: {
    poster: {
    }
  }
}
</script>

<style lang="scss">
$green-button-color: #99D17B;
.maximized {
    background-color: rgba(15, 15, 15, 80%);
    position: fixed;
    top: 10%;
    bottom: 0px;
    height: 100%;
    width: 100%;

    &__img {
      margin-top: 1%;
        height: 50%;
        margin-bottom: 1%;
        width: inherit;
        object-fit: contain;
    }

    &__text {
        margin-left: 30%;
        font-family: 'Roboto', sans-serif;
        font-size: 18px;
        color: #f1f3f4;

        &_aligned-right {
            float: right;
            text-align: left;
            margin-right: 40%;
        }
    }

    &__download-button {
        margin-left: 100px;
        margin-top: 160px;
        font-size: 62px;
        padding-left: 30px;
        padding-right: 30px;
        background-color: $green-button-color;
        border-radius: 30px;
        border: none;
        outline: none;
        cursor: pointer;

     &:hover {
        background-color: #569664;
    }
    }

    &__close-button {
        position: absolute;
        top: 0;
        right: 20%;
        font-size: 80px;
        outline: none;
        background-color: transparent;
        text-decoration: none;
        cursor: pointer;
        color: white;
        text-shadow: black 6px 6px 10px;
        border: none;
    }
}
</style>
