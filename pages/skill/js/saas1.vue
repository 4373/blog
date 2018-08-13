<template>
  <div>
    <h2 class="title">SaaS项目 结后总结1</h2>
    <p class="text-center">2018-08-13 by me</p>
    <p>从去年九月开始到今年7月，做了个SaaS项目。这个项目基本是独立完成，包括环境的搭建，权限的设计，单据的打印等。总之写完之后还是收获了很多，如今赶上开始写博客，正好记录下来。</p>
    <p>这个项目是用vue-cli脚手架搭建的单页面应用。 其中包括一些vue的周边vue-router， vuex。ui使用的是element-ui，而数据请求使用的是axios， 还有一些特定功能使用到了e-charts，xlxs，wangEditor等。</p>
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