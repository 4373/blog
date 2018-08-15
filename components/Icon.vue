<style>
    .icon {
      width: 1em;
      height: 1em;
      vertical-align: -0.15em;
      fill: currentColor;
      overflow: hidden;
    }
</style>
<template>
  <svg class="icon" aria-hidden="true" :style='{fontSize: size + "px"}'>
    <use :xlink:href="'#icon-' + type"></use>
  </svg>
</template>
<script>
  export default {
    props: {
      type: {
        type: String,
        default: ''
      },
      size: {
        type: String | Number,
        default: 14
      }
    }
  }
</script>