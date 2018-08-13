<template>
  <div>
      <h1>fdsjfds</h1>
      <h1>fdsjfds</h1>
      <h1>fdsjfds</h1>
      <h1>fdsjfds</h1>
      <nuxt-child></nuxt-child>
  </div>
</template>
<script>
  export default {
    layout: 'home',
    mounted() {
      console.log(this.$route)
    }
  }
</script>