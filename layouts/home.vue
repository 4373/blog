<style>
  body,
  html {
    background: #eee;
    margin: 0;
    padding: 0;
    font-size: 14px;
    color: #665577
  }

  * {
    box-sizing: border-box;
  }

  .icon {
    width: 1em;
    height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
  }

  .index-layout {
    display: flex;
    margin: 1vh;
    padding: 16px;
    border-radius: 10px;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.2);
    min-height: 98vh;
    background: white;
  }

  .layout-left {
    padding: 8px;
    flex: 0 0 180px;
    border-right: 1px solid #eee;
  }

  .layout-right {
    padding: 8px;
    flex: 1 1 auto;
  }
  .head{
    margin-bottom: 16px
  }
  .position-item{
    float: left;
    padding: 0 16px;
    border-left: 1px solid #ddd;
    color: #888
  }
  .position-item:first-of-type{
    border-left: none;
    padding-left:0;
  }
</style>
<template>
  <div class="index-layout">
    <div class="layout-left">
      <img src="~static/logo.png" alt="" height=80>
      
    </div>
    <div class="layout-right">
      <div class="head clearfix">
          <div class="position clearfix left">
              <span class="position-item">
                <svg class="icon" aria-hidden="true">
                    <use xlink:href="#icon-home"></use>
                </svg>
                <span class='ml-1'>首页</span>
              </span>
              <span class="position-item">
                  <svg class="icon" aria-hidden="true">
                      <use xlink:href="#icon-js"></use>
                  </svg>
                <span class='ml-1'>JS</span>
              </span>
              <span class="position-item">
                  <svg class="icon" aria-hidden="true">
                      <use xlink:href="#icon-article"></use>
                  </svg>
                <span class='ml-1'>this 的一切</span>
              </span>
          </div>
          <div class="right">
              <svg class="icon" aria-hidden="true">
                  <use xlink:href="#icon-user"></use>
              </svg>
          </div>
      </div>
      <nuxt></nuxt>
    </div>
  </div>
</template>
<script>
  export default {
    head: {
      link: [
        { rel: 'stylesheet', href: '//at.alicdn.com/t/font_789693_qhjr2o02p8.css' }
      ],
      script: [
        { src: '//at.alicdn.com/t/font_789693_m7bduh5vm.js' }
      ]
    },
    data() {
      return {}
    },
    mounted() {
      console.log(this.$route)
    }
  }
</script>
