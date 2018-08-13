<template>
  <nuxt-child></nuxt-child>
</template>
<script>
  export default {
    layout: 'home',
    mounted() {
      console.log(this.$route)
    }
  }
</script>